# Running Jellyfin Behind a Reverse Proxy

It's possible to run Jellyfin behind another server acting as a reverse proxy.  With a reverse proxy setup, this alternative server handles all network traffic and proxies it back to Jellyfin.  This has the benefit of having nice DNS names and not having to remember port numbers, as well as easier integration with SSL certificates.

A reverse proxy is a server, usually a web server or dedicated application, that handles network traffic coming in from clients and proxies it back to Jellyfin, instead of the user connecting directly. This has a number of benefits, such as:

* Nicer ports - you can use port 80 or 443 for your Jellyfin instance, without reconfiguring Jellyfin itself or running it as an administrative user.
* Nicer DNS names - you can use whatever domain(s) you want and have the reverse proxy listen on that domain specifically.
* Request queueing - Jellyfin's built-in HTTP server is generally OK, but it can sometimes be useful for an administrator to queue large numbers of incoming requests.
* Proper SSL support - Jellyfin's built-in HTTP server supports HTTPS operation, but is generally cumbersome especially with services such as Let's Encrypt, which is simplified significantly by using a reverse proxy.
* Chromecast support - Google has deprecated and removed non-SSL HTTP casting in recent versions, so a reverse proxy providing SSL is required in those situations.

A reverse proxy does have some limitations however. Mainly, the URL path must always be `/`, or Jellyfin will not work properly. You should always run Jellyfin on a dedicated subdomain or dedicated port.

The three most popular options for reverse proxies are [Apache](https://httpd.apache.org/), [NGiNX](https://www.nginx.com/), and [HAProxy](https://www.haproxy.com/).

## Apache

Apache is a web server that features reverse proxy support using its `ProxyPass` directive. Apache is one of the most popular HTTP servers, and is very well-documented. The following is a very simple configuration to provide proxying and SSL support, including handling the WebSockets URL.

```
<VirtualHost *:80>
    ServerAdmin master@jellyfin.example.com
    ServerName jellyfin.example.com
    
    Redirect permanent / https://jellyfin.example.com
    
    ErrorLog /var/log/apache2/jellyfin.example.com-error.log
    CustomLog /var/log/apache2/jellyfin.example.com-access.log combined
</VirtualHost>

<IfModule mod_ssl.c>
<VirtualHost *:443>
    ServerAdmin master@jellyfin.example.com
    ServerName jellyfin.example.com

    ProxyPreserveHost On

    ProxyPass "/embywebsocket" "ws://127.0.0.1:8096/embywebsocket"
    ProxyPassReverse "/embywebsocket" "ws://127.0.0.1:8096/embywebsocket"

    ProxyPass "/" "http://127.0.0.1:8096/"
    ProxyPassReverse "/" "http://127.0.0.1:8096/"

    SSLEngine on
    SSLCertificateFile /etc/letsencrypt/jellyfin.example.com/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/jellyfin.example.com/privkey.pem
    Protocols h2 http/1.1

    ErrorLog /var/log/apache2/jellyfin.example.com-error.log
    CustomLog /var/log/apache2/jellyfin.example.com-access.log combined
</VirtualHost>
</IfModule>
```

If you encouter errors, you may have to enable `mod_proxy` or `mod_ssl` support manually.
```
$ sudo a2enmod proxy proxy_http
$ sudo a2enmod ssl
```

## NGiNX

NGiNX is another popular web server. It is far more lightweight than Apache for the same number of connections, and its proxy facilities (using `proxy_pass`) are more robust. The following is a very simple configuration to provide proxying and SSL support. Note that `http2` support was only added in NGiNX 1.9.5; older versions should remove that reference.

```
server {
    listen 80;
    server_name jellyfin.example.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    server_name jellyfin.example.com;
    ssl_certificate /etc/letsencrypt/live/jellyfin.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/jellyfin.example.com/privkey.pem;

    location / {
        proxy_pass http://127.0.0.1:8096;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-for $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Proto $remote_addr;
        proxy_set_header X-Forwarded-Protocol $scheme;
        proxy_redirect off;
    
        # Send websocket data to the backend aswell
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

## HAProxy

HAProxy is specifically a high-availability TCP proxy, including advanced load balancing and health checking functionality. In this respect it is different than both Apache and NGiNX and is far more flexible. HAProxy should be used mostly for advanced configurations, as either Apache or NGiNX is far simpler to administrate. The following is a very simple configuration to provide proxying and SSL support, along with a Layer7 health check to verify that the Jellyfin instance is running.

```
frontend jellyfin_proxy
    bind *:80
# Note that haproxy requires you to concatenate the certificate and key into a single file
## Note that if you're using haproxy 1.8+, you can enable http2 by swapping these lines
##   bind *:443 ssl crt /etc/letsencrypt/live/jellyfin.example.com/complete.pem alpn h2,http/1.1
    bind *:443 ssl crt /etc/letsencrypt/live/jellyfin.example.com/complete.pem
    redirect scheme https if !{ ssl_fc }

    acl jellyfin_server hdr(host) -i jellyfin.example.com
    use_backend jellyfin if jellyfin_server

backend jellyfin
    http-request set-header X-Forwarded-Port %[dst_port]
    http-request add-header X-Forwarded-Proto https if { ssl_fc }
    option httpchk GET /web/login.html HTTP/1.1\r\nHost:\ jellyfin
    server jellyfin 127.0.0.1:8096 check inter 5000
```

You can use the tools `hatop` and `haproxyctl` (installed separately) to view the status of your HAProxy instance, for instance:

```
sudo haproxyctl show health
sudo hatop
[view GUI]
```

