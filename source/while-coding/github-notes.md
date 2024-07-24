# Github notes

## Github authenticating with Git

Your local git repo may be setup with email and username etc, but these are for local git. These do not help with authenticating with platforms like github or gitlab. Using just a git initialized directory, you will be able to clone remote public repositories from these platforms but you will not be able to perform actions like pushing commits, cloning using SSH etc. 

### Cloning a repo

You can clone repo from github using three ways
-  HTTPS: No authentication needed for cloning, so this is the easiest way to clone a repo. But when you try to push a commit, it'll ask for github username and password. In the password, you have to provide personal token (not the password). So, prefer this mode when you plan to work with the repo for short time and mostly for read-only purposes.
-  SSH: Here the authentication with github is required up-front. You have to [setup ssh authentication](#configuring-ssh-key-for-github) even to clone the repo. But once done, you can push commits etc. Prefer this mode when you plan to use the repo for longer time, and not just for read-only purposes.
-  GH CLI

When working with github, you'll need to setup authentication for GitHub in your local git settings 

### setting up github commit signature verification:
- First check that your email id is verified:
  - go to github->user settings->emails->see if it mentions 'unverified' below your email id
  - ref [here](https://docs.github.com/en/github/getting-started-with-github/signing-up-for-github/verifying-your-email-address)
#### signing using SSH key (preferred)
- I am preferring this method as here you can use the same ssh key to authenticate with github as well as to sign the commits. So, you have to manage only one key. And since there is only one key, it is easy to move it to a different machine if you are setting up a new hardware. To move ssh key, you just have to copy the public and private key files from ~/.ssh/ directory to new machine, same directory.
- In this method you can add the same SSH key as signing and authn key in the github settings -> ssh and gpg key section.
- Two setting that you have to change in the local git configuration is as below:
  ```
  
  ```
#### signing using GPG key
- Check if you have a GPG key (private-public key pair) already generated for this email id on your machine
  - `gpg --list-secret-keys --keyid-format LONG`
- if you don't have a key generate it
  - while generating the key, it'll ask for inputs, most of it is ok to keep default and email is your github (preferrably private, or public) email id.
  - `gpg --full-generate-key`
  - ref [here](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification/generating-a-new-gpg-key)
- Now check the key that got generated
  - `gpg --list-secret-keys --keyid-format LONG`
  - output have a line similar to `sec   rsa4096/<your key> 2021-06-02 [SC]`
- Now, set GPG key in your local git client
  - `git config --global user.signingkey <your key>`
- Now we need to add same key to your github account
  - get public key block
    - `gpg --armor --export <your key>`
    - copy the entire text that got printed on your screen, starting from first '-' to last '-'
  - now go to github->profile->settings->SSH and GPG keys->New GPG key. Paste public key block that you copied in step above.
- after this whenever you want to sign a commit add `-S` flag
  - `git commit -S -m your commit message` 
- If you want to move gpg key from some other machine to a new hardware setup, then do following
  - find the id of the key. List the existing keys on current machine as below and `id` is the part after `rsa4096` in `sec   rsa4096/[**YOUR KEY ID**] 2024-03-30 [SC]` 
  - export keys from currect machine
    ```
    # export public key
    gpg --export -a [your key id] > gpg-pub.asc

    # export private key
    gpg --export-secret-keys -a [your key] > gpg-sc.asc
    ```
  - Move these key files to new machine and import keys using
    ```
    gpg --import gpg-pub.asc
    gpg --import gpg-sc.asc
    ```
- Troubleshooting:
  - Many times people face this error while trying to push to github.
  `commits must have valid signatures` 
  this error is saying that you are trying push commits that are unsigned. Many times people confuse it with commits that are already there in github. To solve this you have to find the unsinged commit and sign it. To see all commits with its signing information run `git log --show-signature`.
  - when you run `git log --show-signature`, you'll see that there are lot of red warnings which are like this.
      ```
      gpg: Signature made Monday 25 October 2021 10:10:36 PM IST
      gpg:                using RSA key 4AEE18F83AFDEB23
      gpg: Can't check signature: No public key
      Merge: 2880250f3 f5ec22d37
      Author: YuriyZ <yzabrovarniy@gmail.com>
      Date:   Mon Oct 25 19:40:36 2021 +0300

      ```
      it says `signature made` but no public key available. This is will be the case with commits signed by other members of your team. Because you don't have their public key stored with you. To do so, run `curl https://github.com/ossdhaval.gpg | gpg -import` to download key for user `ossdhaval`.
      
      

Above steps were derived from links given [here](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification)

### issues vs PRs
  
  ##### Issues
  - Used for raising bug or feature requests or tracking large development work
  - Focus is around requesting, planning and tracking tasks and work

  ##### PRs
  - Used for tracking, discussing code changes 
  - Focus is on code and not planning or tracking work

### Linking issues and PRs

##### linking issues with issues
- do it with `issue mentions` or creating issues from `task lists`
##### issues with PRS
- in issue : do it with `linked PR` section on the right
- in PR : you can link issue by using key words like `closes`
- In both you can refer to an issue using number afte #
##### PRs with PRs

### Creating Issue and PR templates that apply to all the repos in org

If you want certain files to be set as default for all the repos under your org, you can create a `.github` repo. Github uses files under this repo as default. Reference [here](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)

##### Issue template

- creat a new repo `.github` in org github account
- To create a new template called `development-item`, create a new file as `.github/ISSUE_TEMPLATE/development-item.md`. This will create two new folders and one file. 
- Put below header in the file and then start writting your contents for template.

```
---
name: Contribution item
about: Developers should use this when contributing a feature or bug fix
title: ''
labels: ''
assignees: ''
---
```

- create another template in `ISSUE_TEMPLATE` directory in similar way. For example `feature-request.md`
- You may have to enable templates from `settings` of `.github` repo as well. But not sure if this step is required. Ideally, after the first step, whenever you create a new issue, git hub should first show you a screen to select the issue template.

##### PR template
- Create a PR template file named `pull_request_template.md` under `.github` repository root folder. 
- Not tried: if you have more than one pull request templates, you should put it under `PULL_REQUEST_TEMPLATES` folder



reference [here](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates).


### code owners
- you can define code owners by creating `CODEOWNERS` file in target branch.
- code owners are specific to branch and hence you can have different code owners per branch
- There are two things that code owners file can help with 
  1) when you raise a pull request, the code owners as defined in base branch will get review requests
  2) when you have turned on branch protection for that branch from `settings` of repo, you can require approval from code owner of that branch for all PRs before merging.


### Repository defaults
- you can define following as default for every new repository in your org
  - Labels
  - default branch name
- this can be done from organization settings -> repository defaults


### Security

- have SECURITY.md in .github repository at org level, like [this](https://github.com/falcosecurity/.github/blob/master/SECURITY.md)
- enable security advisory in github, like [this](https://github.com/falcosecurity/.github/security)
- Enable Dependabot scanning
- read process around [security vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/about-github-security-advisories)
- [Best practices](https://docs.github.com/en/code-security/security-advisories/about-coordinated-disclosure-of-security-vulnerabilities)


### Labelling :

- [good artice](https://seantrane.com/posts/logical-colorful-github-labels-18230/#:~:text=Issue%2FPR%20labels%20should%20only,intuitive%20at%2Da%2Dglance.)
- [good discussion about maintaining labels](https://github.com/kubernetes/community/issues/2032)
- check this [labeler](https://github.com/actions/labeler)


### github api:

you can get programatic access to github data using rest api. For example, to get all repositories in JanssenProject org:

```
curl  https://api.github.com/orgs/JanssenProject/repos
```


### using github rest api

Till version 3, github had rest apis but from version 4 they have moved to GraphQL. 

#### using version 4 (graphQL API)

- Reference : https://docs.github.com/en/graphql
- public schema: https://docs.github.com/en/graphql/overview/public-schema
- how to use without explorer: https://docs.github.com/en/graphql/guides/forming-calls-with-graphql
- how to use : https://docs.github.com/en/graphql/guides/using-the-explorer
- explorer url: https://docs.github.com/en/graphql/overview/explorer

#### using rest API

all APIs are listed https://docs.github.com/en/rest/reference

you can access public data without authenticating. For example:

```
curl https://api.github.com/users/ossdhaval
```

but to access some information plus to make changes to github data you have to authenticate.


##### authentication

Your regular ssh key will not work. You have to get an OAuth key or [generate a personal token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token).

Then you can fire command using curl

```
curl -u ossdhaval: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 -H "Accept: application/vnd.github.zzzax-preview+json" https://api.github.com/repos/ossdhaval/gitcheck/branches/main/protection/required_signatures
```

### Useful Tools 
- for analysing github data of your org and multiple repos: https://livablesoftware.com/tools-mine-analyze-github-git-software-data/
- Agile project management on github: https://www.zenhub.com/

### github repository permission levels
https://docs.github.com/en/organizations/managing-access-to-your-organizations-repositories/repository-permission-levels-for-an-organization

### github change log (audit log)
you can see all the changes that happend to all the entites in your organisation in github using audit logs. You need to be organization `owner` to
be able to see this.
https://docs.github.com/en/organizations/keeping-your-organization-secure/reviewing-the-audit-log-for-your-organization#accessing-the-audit-log


### branch protections

- `Require status checks to pass before merging`
  - at this time, when you turn on this protection, only statuses that were run in last week will be available for selection in the search box. so if there is an active status check but corresponding workflow did not run during last week then that status check will not be available for selection
  - name of the status check is the name of the job within workflow or externally injected status
- only jobs from those workflow will be appear in search selection box which get triggered on [pull-request] event

a good link for troubleshooting: 

https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/troubleshooting-required-status-checks

### useful shortcuts

- `e`	Open source code file in the Edit file tab
- `ctrl+s` write commit message
- `.` to open Quick IDE at github.dev
- `ctrl+k` to open command palette

[full list](https://docs.github.com/en/get-started/using-github/keyboard-shortcuts#about-keyboard-shortcuts)


### How to split a big PR into smaller PRs

- there is no direct way of doing this as Github only allows one PR per branch. To solve this problem, you have to move changes into separate branch and create a PR from there.
- So if you have a branch `big-branch` from master with three changes `c1`, `c2` and `c3` and a PR has been created on top of that then you have to follow two step process
  - Create new branch from parent of `big-branch` and call it `b1`. We want to move change `c1` to `b1` 
  - and then remove `c1` from `big-branch`

##### move `c1` to `b1`

- Create a branch `c1` from `main`. `main` is parent of `big-branch`.
- switch to `b1`
- Now cherry pick commit/commits related to `c1`

##### remove `c1` from `big-branch`
- 

### Ways to interact with Github
  - [UI](https://github.com/)
  - [REST API (V2)](https://docs.github.com/en/rest)
  - [GraphQL API (V3)](https://docs.github.com/en/graphql)
  - [Github CLI](https://cli.github.com/)
  - [Github libraries](https://docs.github.com/en/rest/overview/libraries)

### Efficient and power user tips
- Give comments quickly with [saved responses](https://docs.github.com/en/github/writing-on-github/working-with-saved-replies/about-saved-replies)


### questions or missing features:
- how to know which all PRs are containing changes for a particular file? At times what happens is that same file is being changed in multiple PRs that leads to merge conflicts later on.
- sometimes it happens that after looking at file content you want to know who changed this piece of text? there should be a way to find commit and PR that changed that part in file
- We need codeowner groups. So that review can be requested from a group and if anyone from that group gives approval, that should be sufficient (configurable).


### search for issues or PR excluding certain words
- `is:pr is:open NOT chore NOT Snyk` will give you all open PRs which doesn't have word `chore` or `Snyk`

### emoji list
https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md#emoji-cheat-sheet
just type `:` followed by a search character in github issues, PRs, comments etc and any .md file and github will show a list of emojis

### list of shields that you can use in your readme or other files on github
https://shields.io/

### Github recommendations around file sizes, repo sizes 
https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github

I couldn't find any guidelines online so I took a screenshot and saved it as png to check the size. It came out to be 400kb. So I recommended 1MB max size and png as format.


### how to create an internal pull request from a PR from a fork
- This was required when we had a limitation from sonarcloud integration where sonarcloud analysis will not trigger on a PR coming from a fork
- Basic flow is
  - `xyzuser` has forked your repo `forkthis`
  - `xyzuser` has pushed code into `main` branch of his fork.
  - `xyzuser` has created PR on `main` branch of your `forkthis`
  - once you have received a PR from a fork, you create another branch from `main` of `forkthis`
    ```
    git switch main
    git branch review-external-pr
    git switch review-external-pr
    ```
  - then you pull the changes from feature branch of the PR (i.e xyzuser/forkedrepo and my-fix branch)
    ```
    git pull git@github.com:xyzuser/forkedrepo.git my-fix
    ```
  - Now your branch has all the changes from `xyzuser` and you can create another PR which will be an internal PR based on a branch instead of a fork

reference: https://gist.github.com/Chaser324/ce0505fbed06b947d962#manually-merging-a-pull-request


### PR merge commits
When you raise a PR, Github create a new commit behind the scene to see how merged code will look like. So, you can checkout PR in two versions:
- unmerged version of code, represented by head: `refs/pull/<number>/head`
- Code merged with target branch, represented by merge: `refs/pull/<number>/merge`
when you are looking at diff in github for a PR, you are looking at diff of how it'll look after merging your branch with base branch.

Plus, github action `checkout` action by default checks out merge commit and runs actions on that. So, when actions run, they are running on code from your branch plus code from base branch. See the GH action log below. Second last line is sayting that it has checked out a commit which is merge of two commits, one from current branch and another from base branch:

```
Run actions/checkout@v3
Syncing repository: JanssenProject/jans
Getting Git version info
Deleting the contents of '/home/runner/work/jans/jans'
Initializing the repository
Disabling automatic garbage collection
Setting up auth
Fetching the repository
Determining the checkout info
Checking out the ref
  /usr/bin/git checkout --progress --force refs/remotes/pull/1123/merge
  Note: switching to 'refs/remotes/pull/1123/merge'.
  
  You are in 'detached HEAD' state. You can look around, make experimental
  changes and commit them, and you can discard any commits you make in this
  state without impacting any branches by switching back to a branch.
  
  If you want to create a new branch to retain commits you create, you may
  do so (now or later) by using -c with the switch command. Example:
  
    git switch -c <new-branch-name>
  
  Or undo this operation with:
  
    git switch -
  
  Turn off this advice by setting config variable advice.detachedHead to false
  
  HEAD is now at bf42446c2 Merge 4ed88dd504315988fc8114535068d7db8e57043d into 41b6fa185505d3a6a1b5423a6f6df38337a14168
/usr/bin/git log -1 --format='%H'
'bf42446c2ea150faaabcb4037eb1e625a4b4016d'
```

### Difference between release vs tag in github

Ref : https://stackoverflow.com/a/18512221/2331225

In short, tag is a Git concept. It points to a commit and can be enriched by more content like creator etc
While `release` is a GH concept built on top of tag. While creating release from a tag, you can add release notes, artifacts etc.

About backporting changes to old tag/release:
ref: https://stackoverflow.com/a/21466838/2331225

```
You can't put a new commit into an existing tag without breaking an important Git guideline: Never(*) modify commits that you have published.

Tags in Git aren't meant to be mutable. Once you push a tag out there, leave it alone.

You can, however, add some changes on top of v1.1 and release something like v1.1.1 or v1.2
```

## GitHub reference material:
- Mohammad abu's github cheatsheet: https://medium.com/@moabu/the-github-cheat-sheet-df4b3e3b42a8


## Notifications

- Inbox : the number shown besides `inbox` on left menu is just unread messages (not all the messages). So, when you mark a notification in `octobox` as `read` by pressing `d` (and click synch button), it reduces that number on github as well, but remember that the notification is still in the `inbox`. You can see all the messages in GH inbox by clicking `all` button on GH.
- There is no way to mark something `done` using octobox directly.
- Mute on octobox also mutes a notification on GH

## Guidelines for Good PR and communication

https://github.blog/2015-01-21-how-to-write-the-perfect-pull-request/

There two points that are good:

- Be aware of negative bias with online communication. (If content is neutral, we assume the tone is negative.) Can you use positive language as opposed to neutral?
- Use emoji to clarify tone. Compare “sparkles sparkles Looks good +1 sparkles sparkles” to “Looks good.”

Another good article: https://github.com/alphagov/styleguides/blob/master/pull-requests.md


## issue resolved comments are useful

See the comment at the end of [this issue](https://github.com/dcoapp/app/issues/69). It is really useful when people know when a fix was available for that particular issue.

![image](https://github.com/ossdhaval/mysite/assets/343411/904f7cec-5364-40e4-9401-89231b642e36)

## Pull request reviews: approving reviews Vs non-approving reviews

when someone reviews and approves a PR, based on who is providing the approval, the review can be considered `approving`. See in [this PR]() image below, there are three reviewers. PR needs two approving reviewers to be able to merge. Though two out of three reviewers have given the approval, the PR was not ready to merge as one of the reviewer who gave the approval was not an `approving reviewer`.

![image](https://github.com/ossdhaval/mysite/assets/343411/7ac02b30-90d3-40a2-94d4-033c916fd019)

In the image above, you see that one of the review approval is shown as green tick while the other one is grey. Green one is from an approving reviewer, which the other one is from a normal user.

I still have to find out what makes a reviewer an `approving` reviewer, but CODEOWNERs attached to that PR are surely the `approving` reviewers.

## Github graphql queries

Use these queries at: https://docs.github.com/en/graphql/overview/explorer

### get issues and PRs raised by you between two dates

```text
{
  viewer {
    login
    contributionsCollection(from:"2024-03-31T00:00:00Z", to:"2024-04-05T00:00:00Z") {
      issueContributions(first: 100) {
        edges {
          node {
            occurredAt
            issue {
              id
              title
            }
            
          }
        }
      }
      pullRequestContributions(first:100){
                 edges{
                  node{
                    occurredAt
                    pullRequest{
                      title
                  }
                }
             }
          }
      
        }
      }
    }


```


## configuring ssh key for GitHub

- create a key
  ```
  ssh-keygen -f ssh-key-github-ed25519-ossdhaval -t ed25519 -C "343411+ossdhaval@users.noreply.github.com"
  ```
- Open the public key file
  ```
  cat ~/.ssh/ssh-key-github-ed25519-ossdhaval.pub
  ```
  copy the content of this
- Add public key to GitHub
  - go to your github account on web > settings > ssh and gpg keys > add ssh key
  - paste the public key content copied above
- On your machine, start the ssh-agent
  ```
  eval `ssh-agent`
  ```
  This will show a PID.
- add your private key to ssh agent
  ```
  ssh-add ~/.ssh/ssh-key-github-ed25519-ossdhaval
  ```
- Then test authentication with github
  ```
  ssh -T git@github.com
  ```
  This should show a message like below if the authn is successful.
  ```
  Hi ossdhaval! You've successfully authenticated, but GitHub does not provide shell access.
  ```
