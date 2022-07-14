# Git commands

*Git initial setup* :

`git config --global user.name "Dhaval Desai"`

`git config --global user.email ossdhaval@github.com`

`git config --list`


*Git command for finding details of which remote repo you are currently working with* :

`git remote -v`
or
`git remote show origin`
 

*Adding a remote* :

`git remote add origin https://github.com/ossdhaval/angular-getting-started.git`

*Command to change the url pointed by 'origin'* :

`git remote set-url origin https://github.com/ossdhaval/gsg-giftrecommender-service.git`

Command to rename remote repo
git remote rename origin jans-home

Command to get help on any git command :

git help pull

or to see usage of a git command :

git add -h

clone existing repo :
git clone https://github.com/libgit2/libgit2

Deleting files from your workspace that are commited or pushed :
git rm <filename>

Deleting directory ( and files inside them ) from your workspace that are commited or pushed :
git rm <dirname> -r

Note : difference between removing files directly from file system Vs 'git rm' :
If you remove file directly, it becomes an untracked change in 'git status' which then you
have to do a 'git add'. While 'git rm' will do these two steps in one go. You'll see that 
after 'git rm' the deletions are already staged for next commit.

Moving files and directories :
git considers a movement as renaming. So, if you move a file using simple 'mv' command
then it becomes a untracked changed that you have to add to the staging area. If you do 
it using 'git mv' then it'll move the file and stage it as well for next commit.

to move a file from sub-directory to current dir :
git mv gsg-event-service/pom.xml .

To move a directory ( and all file in it ) from a subdirectory to current dir :
git mv  gsg-event-service/src .

To avoid entering username and password everytime when you do git push :
git remote set-url origin https://ossdhaval:open\$5github@github.com/ossdhaval/gsg-shared-kernel.git
note that the '\' before $ is because $ is considered as special character and hence needed an escape character.



get current commit history of your local active branch ( HEAD points to local active branch )
`git log HEAD`
Note : HEAD is case-sensitive

get current commit history of your remote branch ( origin usually points to branch that is your current remote  )
`git log origin`
 
to see what code actually changed use 'patch' option. 
`git log --patch`

to limit commits use option
`git log -8`

 To see status of all files with short representation of status :
git status --short


To add all untracked and modified tracked files and folders recursively in git staging area ( ready for next commit )
git add -A
( 'git add' will just do it for files in current directory and not recursively )


To remove a file after adding it to tracked changes using 'git add'
git reset <file_name>

Branch information :
 
 Remember: HEAD is a pointer to a branch, and a branch is a pointer to a commit.
 So when you say `git commit`, git first looks at where the HEAD is pointing, and then it'll move that branch pointer to point to new commit. 

There are two useful command to understand current branches and their status more :
git log --oneline --decorate --all
and 
git remote show origin

First command shows which all branches you have in local, at which commit they are pointing to, and which one is your current working directory branch ( pointed to by HEAD ). 
 
`dhaval@thinkpad:~/IdeaProjects/Janssen/home$ git log --oneline --decorate --all`
```
a81b684 (origin/main, origin/HEAD) Update Gemfile
1c345e4 Merge branch 'main' of https://github.com/ossdhaval/mysite
37009fd Update Gemfile
37210da (HEAD -> gh-pages) Update _config.yml to fix the description
9839c2a Update _config.yml
ec2ca67 Set theme jekyll-theme-cayman
647f71c (origin/gh-pages) Update index.md
75894c8 Update index.md
b25aef9 Update RELEASE_NOTES.md
51bed95 Update index.md
931132e Create RELEASE_NOTES.md
```


Second command tells you about remote repository. And what is current state with respect to local branches.
 
`:~/IdeaProjects/Janssen/home$ git remote show origin`
 ```
* remote origin
  Fetch URL: https://ossdhaval:open$5github@github.com/ossdhaval/mysite.git
  Push  URL: https://ossdhaval:open$5github@github.com/ossdhaval/mysite.git
  HEAD branch: main
  Remote branches:
    gh-pages                            tracked
    main                                tracked
    refs/remotes/origin/viagluu-patch-1 stale (use 'git remote prune' to remove)
  Local branch configured for 'git pull':
    main merges with remote main
  Local refs configured for 'git push':
    gh-pages pushes to gh-pages (local out of date)
    main     pushes to main     (local out of date)
dhaval@thinkpad:~/IdeaProjects/Janssen/home$ 
```

Branch (i.e tracking branch) :

Most of the local branches that get created during clone are tracking branches. Which means they are tracking a remote branch. You can see which local tracking branch is tracking which remote branch, you can do it with 
```
git branch -vv 
```

 
### local branches, remote tracked branches, branches on remote server
 
 In git, code can reside on your local machine or some remote server. Both local machine and remote can have branches that other one don't know about. Branch that is in local machine is called 'local branch', branch that is in remote server is called 'remote branch'. Git also maintains remote-tracking branches on your local machines for every remote that you have. This is essentially download of all the branches and code that was on remote server when you connected with it last time using `fetch` (or `pull`).
 
Now, you can link-up your local branch to a remote tracking branch for ease of use. If you do, git automatically knows which remote branch a local branch pushes to or fetches from. If you want to see which of your local branches are linked to which remote-tracking branches, you can use
 
 ```
 git branch -vv
 ```
 
 #### About local branches:
 - you can create a simple local branch that doesn't link to any remote tracker using `git branch <name>`
   - Remember that changes in the current branch that you haven't committed yet will also be part of new branch
 - Start using this branch by switching to it: `git switch <name>`
 - Remember, even if your local branch is not tracking a remote tracking branch, you can still use it to work with any remote branch. It is just that you have to mention which remote and which branch of that remote should be used for that operation everytime. I recommend this manual approach as it makes it clear where your code is going and coming.
 - To make local branch track a remote branch: `git branch -u <remote>/<branch> <local-branch>`
 
 
 
### create branch localy and push it to github
 
`git checkout -b 'feature-1'` - Create and switch to new branch
 
`git push --set-upstream origin feature-1` - this will create a new branch on remote 'origin' and set that new branch as upstream
branch for local branch.

```
 
dhaval@thinkpad:~/IdeaProjects/ossdhaval/github-action-check$ git checkout -b 'feature-1'
Switched to a new branch 'feature-1'
dhaval@thinkpad:~/IdeaProjects/ossdhaval/github-action-check$ git status
On branch feature-1
nothing to commit, working tree clean
dhaval@thinkpad:~/IdeaProjects/ossdhaval/github-action-check$ git push origin
fatal: The current branch feature-1 has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin feature-1

dhaval@thinkpad:~/IdeaProjects/ossdhaval/github-action-check$ git push --set-upstream origin feature-1
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'feature-1' on GitHub by visiting:
remote:      https://github.com/ossdhaval/git-action-check/pull/new/feature-1
remote: 
To https://github.com/ossdhaval/git-action-check.git
 * [new branch]      feature-1 -> feature-1
Branch 'feature-1' set up to track remote branch 'feature-1' from 'origin'.
dhaval@thinkpad:~/IdeaProjects/ossdhaval/github-action-check$ 
 
```

`git push origin main` what this command actually is this `git origin master:master`. Which means take my *master* branch and push it to *origin*'s master branch. Using this you can also push changes in your master branch to some other branch on remote.
 
 
#### How to know which branches can be deleted?
 
The useful --merged and --no-merged options can filter this list to branches that you have or have not yet merged into the branch you’re currently on. To see which branches are already merged into the branch you’re on, you can run git branch --merged:

```
$ git branch --merged
  iss53
* master
```

Because you already merged in iss53 earlier, you see it in your list. Branches on this list without the * in front of them are generally fine to delete with git branch -d; you’ve already incorporated their work into another branch, so you’re not going to lose anything.

 Likewise, to see branches that has unmerged changes:
 
```
git branch --no-merged
```

#### How to completely remove local branch and remote-tracking branch and start fresh from remote branch:
 
 In case you have messy code in your local branch that you have committed but not pushed to remote. You want to get rid of this code and start afresh from remote branch. For this you have to 
 1) Delete local branch: `git branch -D file-sync-22-master-1623760119`. Check using `git branch -vv`
 2) Delete local remote-tracking branch: `git branch -dr origin/file-sync-22-master-1623760119`. Check using `git remote show <remote-name>`
 3) Get remote branch in local tracker branch again: `git pull`. Check using `git remote show <remote-name>`
 4) Create new local branch from newly created local remote-tracking branch: `git checkout -b file-sync-22-master-1623760119 origin/file-sync-22-master-1623760119`. Check using `git branch -vv`.
 
 `ref:` https://stackoverflow.com/a/23961231/2331225
 
 
 

 
Avoiding to use .gitignore for your custom file :

In a large project, everyone shares the same gitignore file which is commited and maintained in repository just like any other common code file. I you want to add few custom ignores to this file, it'll affect everyone. To avoid this, use below :

https://medium.com/@dave_lunny/exclude-files-from-git-without-committing-changes-to-gitignore-986fa712e78d


My co-worker pointed me to the .git/info/exclude file which, much like a .gitignore file, allows you to ignore files from being staged. This keeps things nice and clean, and the best part is that you don’t commit anything in the .git/ directory, so it’s like your own personal .gitignore that no one else can see or touch!

gitignore general guidlines :

Setting up a .gitignore file for your new repository before you get going is generally a good idea so you don’t accidentally commit files that you really don’t want in your Git repository

In the simple case, a repository might have a single .gitignore file in its root directory, which applies recursively to the entire repository. However, it is also possible to have additional .gitignore files in subdirectories. The rules in these nested .gitignore files apply only to the files under the directory where they are located.

GitHub maintains a fairly comprehensive list of good .gitignore file examples for dozens of projects and languages at https://github.com/github/gitignore if you want a starting point for your project.

some useful patterns :

### ignore all .a files
*.a

### but do track lib.a, even though you're ignoring .a files above
!lib.a

### only ignore the TODO file in the current directory, not subdir/TODO
/TODO

### ignore all files in any directory named build
build/

### ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

### ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf

How to see what changes have you made to files and are not staged or staged but are not commited :

git diff

To see what you’ve changed but not yet staged, type git diff with no other arguments

If you want to see what you’ve staged that will go into your next commit, you can use git diff --staged. This command compares your staged changes to your last commit

 
 
To push your changes to remote repo :
git push remote-name branch-name
example: git push origin master
this will ask for github username and password. 

Guidlines for git commit messages from PRO-git:

The last thing to keep in mind is the commit message. Getting in the habit of creating quality
commit messages makes using and collaborating with Git a lot easier. As a general rule, your
129messages should start with a single line that’s no more than about 50 characters and that describes
the changeset concisely, followed by a blank line, followed by a more detailed explanation. The Git
project requires that the more detailed explanation include your motivation for the change and
contrast its implementation with previous behavior — this is a good guideline to follow. Write your
commit message in the imperative: "Fix bug" and not "Fixed bug" or "Fixes bug."
 
More guidelines for commit messages:
 https://robertcooper.me/post/git-commit-messages

How to troubleshoot : 'Your branch and 'origin/master' have diverged' problem.

this is because the your branch has commits that are not built on top of commits currently available in same branch on origin(remote).  i.e : master branch in your local repo vs master branch in remote repo.

head(master)    : commit1, commit2, commit3, commit5
origin(master)  : commit1, commit2, commit3, commit4
It may be because while you were working on code changes for commit5 in your local repo and committed to local repo, the remote branch moved on due to somebody else pushed changes in it. 
At this point, if you do a 'git status', you get above message.

dhaval@dhaval-Lenovo-U41-70:~/code/eclipse-workspace/gsg-event-service$ git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

Now there are two solutions : rebase or merge.
Since merge creates a non-linear history, rebase is preferred by many.
rebase essentially brings in commit5 from remote into your local repo and then puts back commit4 on top of that. To use this option :
git pull --rebase


See the https://stackoverflow.com/questions/2452226/master-branch-and-origin-master-have-diverged-how-to-undiverge-branches/2452610

How to remove files from 'Changes not staged for commit' category of git status :
git checkout <file>

git checkout essentially overwrites your local modified file by latest copy from local branch.


how do you know if you have committed changes in your local branch but not pushed to remote :
Run git status.  Message would say that 'your local is ahead of remote by x number of commits'

Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

This means you have one commit that you have not pushed. 

To see what is going to get committed in next push :
git log --stat

This will give you history of commits. From this history, you can see one commit that are marked with (head->master), and then few commits down the line, you'll see a commit marked with (origin/master, origin/HEAD). 
In the next push, your commit marked with (head->master) and all the commits till and not including (origin/master, origin/HEAD) will be pushed. 


Different file states in git :


Unstaged : untracked files + modified tracked files
git add
Staged : files that are ready to go in next commit
git commit
Committed files to local branch
git log --stat
Pushed to remote repo
git log --stat

Git file moving through various states :

when you create a new file, it is untracked :







now make this a tracked file :







Now to change it back to untracked :







To untrack everything which is there in staging area :

git reset


How to remove files from 'Changes not staged for commit' category of git status :
git restore <file>
or
git checkout <file>
git checkout essentially overwrites your local modified file by latest copy from local branch.


add to the staging area :










modified of the already updated file, just for the completeness of the example :





























to move back to previous state :




























Now commit these files to local git branch :









see your commit in local branch log :


















Now roll back commit which still in local brach and not pushed to shared repo :
git reset --soft HEAD~ 
( --mixed will undo the commit + it'll unstage the changes from staging area,  but will leave changes in the working copy as is.
--hard will undo the commit, unstage the changes and update the working copy with what is in the local branch)












x`





Now push commit to remote repo 



First commit them back in :






see Git log to confirm what is going to get pushed :


















Now push to remote :





















check the git log of remote repo to see that the commit has been made :







Now undo commit from remote repo :
(ref: https://gist.github.com/gunjanpatel/18f9e4d1eb609597c50c2118e416e6a6)

first check if you are on the right branch by running git status. Then 
git reset a81b684513aa2d3faa2cced70460797cc8397528 --hard

(here commit number is the commit which you want to point to going foward. i.e all the commits after
this one will be removed from github, also from insights>network )

and then run :
git push origin main -f

This can also be done using revert :
git revert a81b684513aa2d3faa2cced70460797cc8397528
this will not rewrite the history unlike reset above



storing your changes in a separate branch :

Suppose you are working on branch B1. You have made changes to certain files. You now think that these changes are not required for now and you want to store these changes as a separate branch and come back to B1 and start working on that. For example : I was working on a project where first I tried to integrate with RDBMS using JPA. All these changes were pushed to B1. Then I started to make changes on my local to integrate with DynamoDB instead of RDBMS. But that didn't go well. So, Now I wanted to go back to last commited changes on B1 without loosing my DynamoDB changes. So I decided that I'll create a new branch and store DynamoDB changes on a that branch. And then again switch back to B1 and continue working on RDBMS. Below is the sequence of commands that helped.

git branch NoSQL
git checkout NoSQL

now you'll see that master, NoSQL and origin/master are on the same commit using 'git log'

commit 009ed95a6d83e5b899b5c864a8b84bf72cbb4740 (HEAD -> NoSQL, origin/master, master)

git status

git add .

git commit -m 'Initial attempt at sing DynamoDB'

git push origin NoSQL

git checkout master

In case you have made direct changes in your code from github ( or someone else has committed changes in the branch ) and you want to make your local branch updated with those changes then :
git checkout
Your branch is behind 'origin/dhaval-development' by 40 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
git pull
Username for 'https://github.com': ossdhaval
Password for 'https://ossdhaval@github.com': 
Updating 17e6c35..579473e
Fast-forward
 Jenkinsfile  | 24 ++++++++++++++++++++++++
 package.json |  9 +++------
 2 files changed, 27 insertions(+), 6 deletions(-)
 create mode 100644 Jenkinsfile


`git fetch <remote>` brings all data about that remote to your local machine, including references of new branches that are created on remote server by others.
 
`git fetch <remote> <branch>` brings data from remote only about a particular branch.
 
### Using git fetch and merge instead of pull:
 
While the `git fetch <remote>` command will fetch all the changes on the server that you don’t have yet, it will
not modify your working directory at all. It will simply get the data for you and let you merge it
yourself. However, there is a command called git pull which is essentially a git fetch immediately
followed by a git merge in most cases.

Generally it’s better to simply use the fetch and merge commands explicitly as the magic of git pull
can often be confusing.
 
Secondly, Suppose there is a branch called `serverfix` on remote server that you don't have.
It’s also important to note that when you do a fetch that brings down new remote-tracking branches, you don’t automatically have local, editable copies of them. In other words, in this case, you don’t have a new serverfix branch — you have only an origin/serverfix pointer that you can’t modify.

To merge this work into your current working branch, you can run git merge origin/serverfix. If you want your own serverfix branch that you can work on, you can base it off your remote-tracking branch:

```
$ git checkout -b serverfix origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

This gives you a local branch that you can work on that starts where origin/serverfix is.



#### Workflow for Contributing to an opensource project :

create a fork

clone that fork in your local machine

then make sure you have this setup so that your fork is updated: 
https://gist.github.com/CristinaSolana/1885435 or
https://stefanbauer.me/articles/how-to-keep-your-git-fork-up-to-date

#### To view files in some other branch without switching from your branch
 
Syntax:
 
```
git show branch-name:relative-path-of-file
```

Example:

```
git show pull-request-decoration:.github/workflows/build-with-coverage.yml

```
 
#### To store credentials for 18 hours:

```

git config --global credential.helper "cache --timeout 64800"

```

#### add description to your commit using command line.

 When you fire `git commit` without a `-m`, git will open an editor within terminal. You can put your commit title and description in there. 
 - `git commit` ( or you can continue to use other flags as well like `git commit -S -a` )
 - opens an editor
 - put your commit title after first few commented lines.
 - leave a line blank and then put your description
 - `ctrl+o`
 - enter
 - `ctrl+x
 
#### resolving git merge conflicts:
 
If you are trying to pull some changes and merge conflicts happen then you have two choices:
 1) use commandline to merge using `git merge -t vimdiff`. This will open vimdiff on the terminal and show merge conflicts that you have merge. But this is little
 difficult as it is difficult to navigate commandline.
 2) use Intellij's merge conflict tool. To use it:
  - Press `shift+shift` and then search for 'conflict'. You should see a tool in `git` category.
  - open this tool and then using it you should be easily able to merge. It shows three files.
    - Left: is your local changes
    - Right: is incoming changes
    - Center: is will be the final outcome. This is what you have to edit.
  - Once completed, click apply to apply the changes. 
  - now if you go and fire `git status` then you'll see that your local copy has been modified. You can commit that.

 ### cherry picking:
 
A cherry-pick in Git is like a rebase for a single commit. It takes the patch that was introduced in a commit
and tries to reapply it on the branch you’re currently on. This is useful if you have a number of
commits on a topic branch and you want to integrate only one of them, or if you only have one
commit on a topic branch and you’d prefer to cherry-pick it rather than run rebase.
 
```
 $ git cherry-pick e43a6
Finished one cherry-pick.
[master]: created a0a41a9: "More friendly message when locking the index fails."
3 files changed, 17 insertions(+), 3 deletions(-)
```
 
 Or cherry pick a range of commits. Notice the `^` character at the end of first commit. This is to indicate to git to include that commit as well in cherry pick:
 
 ```
 git cherry-pick dc99f87656a952f3548c320c6459278876f9f7b7^..6967cfc4751c87579c563ba9cbb3721116b72be0
 ```
 if your cherry pick gets a merge conflict, it'll show message as below
 
```
Auto-merging CONTRIBUTING.md
CONFLICT (content): Merge conflict in CONTRIBUTING.md
error: could not apply 2e158b7... docs: update triage section details
hint: after resolving the conflicts, mark the corrected paths
hint: with 'git add <paths>' or 'git rm <paths>'
hint: and commit the result with 'git commit'
```
You can edit conflicted file and resolve the conflict, run `git add` to add that file and then `git commit` to commit that file. But, cherry pick would stop when it finds a conflict and doesn't pick rest of the commits in the range. So, you have to again start cherry pick from where it left. But first you have to stop the previous cherry pick by `git cherry-pick --quit` and then git another cherry pick command with remaining commits as range.
 
 Now you can remove your topic branch and drop the commits you didn’t want to pull in.
 
 > Note: when you cherry-pick a commit, git essentially generates a new commit. And if the original commit had a signature (using -S), then new commit **will not** have that signature. If you want to add signature to new commit as well, use `-S` with cherry-pick as well.
 
### Reset a branch to be same as remote branch
 
 ```
 git reset --hard origin/<branch-name>
 ```

### using sparse checkout to just check out one directory from monorepo
 
```
4581  02/02/22 11:24:08 mkdir jans-evelen
4582  02/02/22 11:24:15 cd jans-evelen/
4583  02/02/22 11:24:20 git init
4584  02/02/22 11:24:37 git sparse-checkout init --cone
4585  02/02/22 11:25:05 git sparse-checkout set jans-eleven
4586  02/02/22 11:25:25 git remote add origin git@github.com:JanssenProject/jans.git
4587  02/02/22 11:26:08 git pull origin main
```

### how to sign commits that you have already pushed to Github
 Reference: https://stackoverflow.com/questions/13043357/git-sign-off-previous-commits
 
 Remember that commit number will change when you do this. So, you'll have to force push to github.
 
 `git rebase --signoff -S HEAD~3` : this will add PGP sign and `signed-off by` message to last three commits
 `git rebase --signoff -S <SHA>` : this is for one particular commit 
 
 after this do `git push --force-with-lease` to push out changes. But one thing that I noticed is that in the PR I could still see previous unsigned commits. I expected those commits to be overwritten.
 
 
 ### why to avoid force push 
 https://blog.developer.atlassian.com/force-with-lease/
 
### git revert
 
### git clean 

### rewriting a commit message
 
 Commit message is part of commit itself, so when you change the message, the commit sha changes. It is like you are creating new commit and replacing old one. 
 
 - if commit has not been pushed: `git commit --amend`
 - If commit has been pushed to remote(GH): Since old commit has already been pushed, you'll have to force push new commit which is a bad practise. So, in this case, you better create a new branch and new PR with good commit. Close the old PR without merging.
 Reference: https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/changing-a-commit-message
 
 ### remove all the untracked files from repo
 
 ```
 git clean -f
 ```
 
 ### check commit signatures 
 
 ```
 git log --show-signature
 ```
