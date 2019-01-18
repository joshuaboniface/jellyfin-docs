# About Jellyfin

Jellyfin is a Free Software Media System that puts you in control of managing and streaming your media. It is an alternative to the proprietary Emby and Plex, to provide media from a dedicated server to end-user devices via multiple apps. Jellyfin is descended from Emby's 3.5.2 release and ported to the .NET Core framework to enable full cross-platform support. There are no strings attached, no premium licenses or features, and no hidden agendas: just a team who want to build something better and work together to achieve it. We welcome anyone who is interested in joining us in our quest!

Jellyfin seeks to continue development of the original Emby project with a Free Software ethos. It is committed to bringing all its users access to the best possible Media System, developed entirely by a community of volunteers who contribute code, documentation, translations, and support to the project. 

The Jellyfin project was started in early December 2018 as a result of Emby's decision to take their 3.6 release closed-source, as well as various philosophical differences with the core developers. Jellyfin seeks to be the free software alternative to Emby and Plex to provide media management and streaming from a dedicated server to end-user devices.

You can find our main repository [on GitHub](https://github.com/jellyfin/jellyfin) as well as [our main organization page](https://github.com/jellyfin).

# Organizational structure

## Philosophy

Jellyfin is a [curated do-ocracy](https://communitywiki.org/wiki/DoOcracy) - the project was started primarily on the initiative of [Andrew](https://github.com/nvllsvm) and [Joshua](https://github.com/joshuaboniface), who act as [benevolent dictators for life](https://en.wikipedia.org/wiki/Benevolent_dictator_for_life) in a co-consul setup. They quickly recruited [Vasily](https://github.com/JustAMan), who was instrumental in completing the .NET Core port of Emby 3.5.2, and [Anthony](https://github.com/anthonylavado), Joshua's friend who was interested in helping out. [Bond-009](https://github.com/Bond-009) was added later for tremendous contributions in the very early stages of the project. It has since grown to over dozen active contributors working in various areas of the project, from the core to the apps.

The core principle of a do-ocracy is that "those willing to do the work lead the project". We seek to embrace this philosophy, while tempering its weaknesses via the stability, direction, and careful review of a Core administrative team and pair of leaders. To this end, organization members are choosen by the administrative team by consensus based on work done and willingness to contribute to the various areas of the project, and when selected are added to one or more of a series of teams, each with specific responsibilities and access to various repositories.

## Code of Conduct

The code of conduct is simple: don't be an ass. We expect users to use professional decorum at all times. While we may disagree over technical decisions, always remember the human on the other side of the screen, and don't act towards them in a way you wouldn't want them to act towards you.

Complaints about a users behaviour or conduct should be directed to Joshua or Andrew as soon as possible. We will investigate and make a determination in private with the user(s) in question and discuss possible remedies.

## Teams

The Jellyfin project makes use of GitHub teams in order to coordinate access and responsibilities throughout the various repositories of the project.

The requirements to join a team are listed in their respective sections, and as described above, positions are granted based on desire to and a successful track record of producing reliable contributions. If selected by the Core team, a person will be contacted directly and invited to join the team, and may accept or refuse as desired. If accepted, the user will be added to the team(s) they desire, and the new organization member will be announced.

Leaving a team or the project as a whole, for whatever reason, should be done via a message to the Core team. As a purely volunteer project, we understand that life can get in the way and that priorities and availability change, and if any team member feels they cannot contribute readily to the project we encourage them to notify the Core team as soon as they can. The Core team reserves the right to remove inactive team members (those without a contribution for at least a month with no contact or explanation), though ideally we will always grow and share the load!

### Core

The Core team consists of the 5 primary administrators of the project, including the leaders. The core team is the only team allowed to perform merges of approved pull requests to the `master` branch, and `dev` branch if applicable, in all repositories, and is responsible the overall direction of the project, handling release coordination, and acting as the central voice and executive committee on behalf of the project as a whole. All disputes, both technical or personal, are settled by the administrative team, with last say by the project leaders.

#### Members

[Andrew](https://github.com/nvllsvm)  
[Joshua](https://github.com/joshuaboniface)  
[Vasily](https://github.com/JustAMan)  
[Anthony](https://github.com/anthonylavado)  
[Bond-009](https://github.com/Bond-009)

### Backend

The backend team consists of those developers who take a strong interest in the server backend (the [jellyfin](https://github.com/jellyfin/jellyfin) repository and related backend libraries and components forked by the project). This core is written primarily in C# and includes the database, transcoding, and user management features.

The team has write access to the mentioned repositories in order to review and approve pull requests. It primarily communicates in the [jellyfin-dev](https://matrix.to/#/#jellyfin:matrix.org) Matrix/Riot channel.

Access to the team is granted for significant contributions to the backend repositories and a demonstrated work ethic towards bettering the project.

#### Members

### UI

The UI (frontend) team consists of those developers who take a strong interest in the user web frontend (the [jellyfin-web](https://github.com/jellyfin/jellyfin-web) repository). The interface is written primarily in Javascript, and is shared both by the main server and the various clients wherever possible. It also includes the translation infrastructure.

The team has write access to the mentioned repository in order to review and approve pull requests. It primarily communicates in the [jellyfin-web-dev](https://matrix.to/#/#jellyfin-web-dev:matrix.org) Matrix/Riot channel.

Access to the team is granted for significant contributions to the UI repository and a demonstrated work ethic towards bettering the project.

#### Members

### App

The App team consists of those developers who take a strong interest in the user apps and their various repositories, or at least one thereof. The apps are written in a variety of languages, and import the jellyfin-web assets wherever possible to avoid code reuse.

The team has write access to the mentioned repositories in order to review and approve pull requests. It primarily communicates in the [jellyfin-app-dev](https://matrix.to/#/#jellyfin-app-dev:matrix.org) Matrix/Riot channel.

Access to the team is granted for significant contributions to at least one client app and a demonstrated work ethic towards bettering the project.

#### Members

[dkanada](https://github.com/dkanada)  
[thornbill](https://github.com/thornbill)  

### Plugin

The Plugin team consists of those developers who take a strong interest in the various forked plugins and their repositories, or at least one thereof. The plugins are written primarily in C#.

The team has write access to the mentioned repositories in order to review and approve pull requests. It primarily communicates in the [jellyfin-dev](https://matrix.to/#/#jellyfin-dev:matrix.org) Matrix/Riot channel.

Access to the team is granted for significant contributions to at least one plugin and a demonstrated work ethic towards bettering the project.

#### Members

### Packaging

The Packaging team consists of those developers who take a strong interest in the packaging of Jellyfin for various platforms. It is currently a part of the core repository.

The team does not have write access to the repository at this time, but it is intended to promote review and approve pull requests to this subsection. At a future date packaging may be split into its own repository, at which point this team will have write access there. It primarily communicates in the [jellyfin-dev](https://matrix.to/#/#jellyfin-dev:matrix.org) Matrix/Riot channel.

Access to the team is granted for significant contributions to at least one packaging system and a demonstrated work ethic towards bettering the project.

#### Members

### Support

The Support team consists of those who take a strong interest in supporting users of the project and assisting them with troubleshooting, issues, and housekeeping of the project.

The team has write access to every repository in order to triage and assign tags to issues, close stale issues, and interface with the other teams via review requests. It primarily communicates in the [jellyfin](https://matrix.to/#/#jellyfin:matrix.org) and [jellyfin-troubleshooting](https://matrix.to/#/#jellyfin-troubleshooting:matrix.org) Matrix/Riot channels.

Access to this team is granted for significant contributions to supporting users on various platforms including Reddit, Riot/Matrix, and in existing issues.

#### Members

## Day-to-day workflow

This section describes the workflow of the various teams through a specific, fictional example, in this case related to the server Web UI. A similar process should be followed for issues affecting other repositories, and the procedure can be slightly modified by e.g. a non-team member requesting ownership of the issue via a comment and submitting a PR, or the same original user who reported the bug doing the same.

1. User Bob reports an issue on Reddit or in Riot

    Bob: Hello, I'm having trouble getting playback to work on my system, I just get a spinning circle.

1. A Support team member, Alice, or another helpful user or contributor, assists Bob in troubleshooting

    Alice: It looks like this is caused by a Javascript failure. Let's try to troubleshoot in #jellyfin-troubleshooting.

1. The troubleshooting determines there is an active issue with Jellyfin, and Alice directs Bob to the issue submission guide

    Alice: Looks like we can see the problem here, it's probably line 123 of file `myjavascript.js`, can you open an issue in our GitHub? If you're not sure, please see our documentation page, or I can open it on your behalf!

1. Bob creates a "Bug" type issue in the [main Jellyfin repository](https://github.com/jellyfin/jellyfin) and reports his details. The issue template automatically attaches the `bug` label.

1. A Support team member (ideally Alice, but otherwise another member, Charles) reviews and triages the open issue by:

   a. Adding the `UI` label.  
   b. Assiging the issue to the UI Team.  
   c. Moving the issue out of the main Jellyfin repository into the [`jellyfin-web` UI repository](https://github.com/jellyfin/jellyfin-web).  

1. A UI Team member, Debbie, sees the open issue in their repository and assignment, and decides this is a bug they can fix. They take ownership by:

   a. Assigning the issue to themselves to acknowledge they are working on this particular bug.  
   b. Working on the issue getting feedback in their Matrix channel(s) as required.  

1. Once the work to correct the bug is done, Debbie submitts a Pull Request to the `jellyfin-web` repository, detailing as per the contributing documentation:

   a. How they fixed the bug.  
   b. What issue(s) the PR is tied to (in this case, Bob's issue).  

1. Debbie assignes the UI Team to review their PR.

1. Another member of the UI Team, Eliot, sees the pending review request, looks over the PR, suggests any changes in a constructive back-and-forth with Debbie, and then approves the PR *with their own name, not on behalf of the team*.

1. With at least one review now completed, either Eliot or Debbie requests review from the Core team on the PR.

1. A Core team member, Joshua, sees the pending review request, looks over the PR, approves the PR or suggests further changes, ensures the title and description are clean and relevant, and then merges the PR.

1. The issue will now automatically close if the PR description is correct.

1. On the next release cycle, the Core team will add the merged PR to the release project board and changelog, indicating that this PR fixed the isssue, and it will be fully closed and resolved.
