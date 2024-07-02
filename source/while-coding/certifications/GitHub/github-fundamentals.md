# GitHub Fundamentals

## References

- 
##### Add a change to last commit without changing the commit message

For example you want to fix a typo that got into the last commit

```commandline
git commit --amend --no-edit
```

##### recover a file after deleting it

- If you have just deleted using `rm`

```commandline
rm myfile.txt
git checkout -- myfile.txt
```

- If you have deleted using `git rm`. In this case, `git rm` has instructed git
  to not track the file anymore. Remember that `git rm` doesn't make a new commit)
  but it just tells git not to track the file anymore.
  At this point if you do `checkout` like before, it'll fail.
  You have to first tell git to start tracking all files as it did in most recent
  commit (HEAD). And then do `checkout` of the deleted file.

```commandline
git rm myfile.txt
git checkout -- myfile.txt (this will fail)
git reset HEAD myfile.txt
git checkout -- myfile.txt (this time it'll be successful and get the file back)
```

## What is Git

What is VCS and SCM?

A version control system (VCS) is a program or set of programs that tracks changes to a collection of files. 
- One goal of a VCS is to easily recall earlier versions of individual files or of the entire project.
- Another goal is to allow several team members to work on a project, even on the same files, at the same time without affecting each other's work.

Another name for a VCS is a software configuration management (SCM) system. The two terms often are used interchangeably—in fact, Git's official documentation is located at git-scm.com. Technically, version control is just one of the practices involved in SCM.

Distributed VCS Vs centralised?

Git is distributed, which means that a project's complete history is stored both on the client and on the server. You can edit files without a network connection, check them in locally, and sync with the server when a connection becomes available. If a server goes down, you still have a local copy of the project.

## Terminologies:

**Working tree**: The set of nested directories and files that contain the project that's being worked on.

**Repository (repo)**: Repo is a directory. The directory, located at the top level of a working tree, where Git keeps all the history and metadata for a project. Repositories are almost always referred to as repos. A **bare repository** is one that isn't part of a working tree; it's used for sharing or backup. A bare repo is usually a directory with a name that ends in .git—for example, project.git.

**Hash**: A number produced by a hash function that represents the contents of a file or another object as a fixed number of digits. Git uses hashes that are **160 bits** long. One advantage to using hashes is that Git can tell whether a file has changed by hashing its contents and comparing the result to the previous hash. **If the file time-and-date stamp is changed, but the file hash isn’t changed, Git knows the file contents aren’t changed**.

**Object**: A Git repo contains **four types of objects**, each uniquely identified by an SHA-1 hash. A blob object contains an ordinary file. A tree object represents a directory; it contains names, hashes, and permissions. A commit object represents a specific version of the working tree. A tag is a name attached to a commit.

**Commit**: When used as a verb, commit means to make a commit object. This action takes its name from commits to a database. It means you are committing the changes you have made so that others can eventually see them, too.

**Branch**: A branch is a named series of linked commits. The most recent commit on a branch is called the head. The default branch, which is created when you initialize a repository, is called main, often named master in Git. The head of the current branch is named HEAD(in caps). Branches are an incredibly useful feature of Git because they allow developers to work independently (or together) in branches and later merge their changes into the default branch.

## Features provided by GitHub on top of Git

Key features provided by GitHub include:

- Issues
- Discussions
- Pull requests
- Notifications
- Labels
- Actions
- Forks
- Projects

**Remote**: A remote is a named reference to another Git repository. When you create a repo, Git creates a remote named origin that is the default remote for push and pull operations.

**Commands, subcommands, and options**: Git operations are performed by using commands like git push and git pull. git is the command, and push or pull is the subcommand. The subcommand specifies the operation you want Git to perform. Commands frequently are accompanied by options, which use hyphens (-) or double hyphens (--). For example, git reset --hard.

## Development and code editing options from GitHub.com  

Github provides three different ways you can edit or develop code from the browser itself. 
- Browsing and editing code from github.com site (good for basic browsing and editing a single file at a time)
- Use github.dev light weight VS code editor to edit code and perform all git operations (Full fledged code browser, editor and can perform all git commands. But can't run, test or debug code)
- Use codespaces, which provides full VS code running on an azure VM with access to shell.


 ### github.dev
- to start, navigate to a repo or a PR on github.com and then hit `dot` (.)
- github.dev is a lightweight VS code editor that can be launched from the browser on your current repo. It is essentially meant to enable all code editing options and git operations. You can't test, run or debug programs there. Also you don't have access to terminal (which you have in codespaces).
- github.dev doesn't have compute attached to it so you can't process your code. Just edit and git operations.
- detailed differences between github.dev and codespaces are described [here](https://learn.microsoft.com/en-us/training/modules/code-with-github-codespaces/4-codespaces-versus-github-dev-editor)

  
### Codespaces

- codespaces is dedicated remote VM on Azure (with compute and storage) with preconfigured VS code (full version) and terminal access
- currently Individuals can use Codespaces for free each month for 60 hours, with pay-as-you-go pricing after that. Teams or Enterprises pay for Codespaces. A maximum monthly cap can also be set for extra pricing control.
- You can customize your project for GitHub Codespaces by committing configuration files to your repository (also known as configuration-as-code), which creates a repeatable codespace configuration for all users of your project. Each codespace you create is hosted by GitHub in a Docker container that runs on a virtual machine. You can choose the type of machine you want to use depending on the resources you need.
- It is not necessary to create a codespace from an existing repo/pr/commit. You can create a blank workspace from a template as well.

### codespaces lifecycle

(create) ----- inactive for 30 mins ---> (Stopped) --- stopped for 30 days --> (deleted)

- You can create codespace
  -  From a GitHub template or any template repository on GitHub.com to start a new project.
  -  From a branch in your repository for new feature work.
  -  From an open pull request to explore work-in-progress.
  -  From a commit in a repository's history to investigate a bug at a specific point in time.
-  If starting a new project, create a Codespace from a template and publish it to a repository on GitHub later.
- You can create more than one Codespace per repository or even per branch.
- When you create a GitHub Codespace, four processes occur:
  -  VM and storage are assigned to your Codespace.
  -  A container is created.
  -  A connection to the Codespace is made.
  -  A post-creation setup is made.
- When you connect to a Codespace through the web, AutoSave is automatically enabled to save changes after a specific amount of time has passed. When you connect to a Codespace through Visual Studio Code running on your desktop, you must enable AutoSave.
- list of your current code spaces: https://github.com/codespaces
- A Codespace requires an internet connection. If the connection to the internet is lost while working in a Codespace, you won't be able to access your Codespace. However, any uncommitted changes are saved. When you reestablish the internet connection, you can access the Codespace in the same state that it was left in when the connection was lost. If you have an unstable internet connection, you should frequently commit and push your changes.
- Only running Codespaces incur CPU charges. A stopped Codespace incurs only storage costs.
- codespaces personlisation: there is a list of things you can personalize [here](https://learn.microsoft.com/en-us/training/modules/code-with-github-codespaces/3-personalize-codespace) but didn't quite understand how to do it.

#### devcontainers

By default, when you start a codespace, it launches a Azure VM and creates a docker container within the VM to host your dev environment. 

You can configure the development container(aka dev containers) for a repository so that any codespace created for that repository will give you a tailored development environment, complete with all the tools and runtimes you need to work on a specific project.

A dev container file(.devcontainer/devcontainer.json) is a JSON file that lets you customize the default image that runs your codespace, VS code settings, run custom code, forward ports and much more!

GitHub Codespaces offers two main ways of personalizing your codespace: Settings Sync with VS Code and dotfiles(this refers to files that start from `.` on any unix, linux system in general).

#### dotfiles

Reference: https://docs.github.com/en/codespaces/setting-your-user-preferences/personalizing-github-codespaces-for-your-account#dotfiles

When you create a new codespace, GitHub clones your selected dotfiles repository(in your GH user settings) to the codespace environment, and looks for one of the following files to set up the environment.
```
install.sh
install
bootstrap.sh
bootstrap
script/bootstrap
setup.sh
setup
script/setup
```
If none of these files are found, then any files or folders in your selected dotfiles repository starting with . are symlinked to the codespace's ~ or $HOME directory.

You need to have all the dotfiles in any one of your GH repositories and mention it under the `settings`->`codespaces`->`enable dotfiles`


## GitHub Projects

- Projects can be at Org level(where there is a GH org), or at repo level. 

### Compare `Projects` Vs `Projects(classic)`

![image](https://github.com/ossdhaval/mysite/assets/343411/9be3748d-d2ae-4f6c-9b75-cff05d7cd160)


**Comprehensive lists of Project enhancements**

-  Tables and boards
  -  Plan and track work in a table or board view
  -  Rank, sort, and group within a table by any custom field
  -  Create draft issues with detailed descriptions and metadata
  -  Materialize any perspective with tokenized filtering and saved views
  -  Customize cards and group-by in Project boards
  -  Real-time Project updates and user presence indicators
-  Data
  -  Define custom fields of type: text, number, date, iteration, and single select
  -  Configure iterations with flexible date ranges and breaks to represent your sprints, cycles, or quarterly roadmap
  -  View linked pull requests and reviewers in both table and board views
-  Insight
  -  Create and configure custom bar, column, line, and stacked area charts
  -  Use aggregation functions like sum, count, average, min, and max to get the proper insight
  -  Persist charts and share them with a URL to keep everyone in the know
-  Automation
  -  GraphQL ProjectsV2 API
  -  GitHub app Project scopes
  -  Webhooks events for Project item metadata updates
  -  GitHub Action to automate adding issues to Projects

### access control

- Project visibility: You have the ability to control whether or not your Project is public or private. When your Project is public, everyone on the internet can view it. When your Project is private, only users granted at least read access can see your Project.
    - If the project is part of an org, then you can also define a `base role` which dictates what is a default role for a member of that org. So if the project is private, but the base role is `write`, then all the members of the org
      would be able to edit the project items. But for people outside of the org, it'll be on invite.
- Who can manage access to your Project
  Admins of organization-level Projects can manage access for the entire organization, for teams, for individual organization members, and for outside collaborators. Admins of user-level Projects can invite individual collaborators and manage their access.

- Organization level Project
  No access: Only organization owners and users granted individual access can see the Project. Organization owners are also admins for the Project.
  Read: Everyone in the organization can see the Project. Organization owners are also admins for the Project.
  Write: Everyone in the organization can see and edit the Project. Organization owners are also admins for the Project.
  Admin: Everyone in the organization is an admin for the Project.
- Personal/User level Project
  Read: The individual can view the Project.
  Write: The individual can view and edit the Project.
  Admin: The individual can view, edit, and add new collaborators to the Project.
