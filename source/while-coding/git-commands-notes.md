# Git commands

*Git initial setup* :

`git config --global user.name "First-name last-name"`

`git config --global user.email myemail@github.com`

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

```

git remote rename origin jans-home

```

Command to get help on any git command :

```
git help pull
```

or to see usage of a git command :

```
git add -h
```

clone existing repo :

```
git clone https://github.com/libgit2/libgit2
```

Deleting files from your workspace that are commited or pushed :
```
git rm <filename>
```

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
 
 to get list of files changed per commit in a branch
 `git log --name-only --oneline`
 
 To get list of contributions grouped by author
 
 `git shortlog`

 To check what all changes a particular file has gone through(even deleted files)

 ```
 git log -- */cli-agama.md
 ```

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
 
 #### About local branches
 
 ##### first option of using untracked local branch
 
 - you can create a simple local branch that doesn't link to any remote tracker using `git branch <name>`
   - Remember that changes in the current branch that you haven't committed yet will also be part of new branch
 - Start using this branch by switching to it: `git switch <name>`
 - Remember, even if your local branch is not tracking a remote tracking branch, you can still use it to work with any remote branch. It is just that you have to mention which remote and which branch of that remote should be used for that operation everytime. I recommend this manual approach as it makes it clear where your code is going and coming.
 - To make local branch track a remote branch: `git branch -u <remote>/<branch> <local-branch>`
 
 ##### second option of using tracked local branch
 
 benefit of this approach is that you know later 
 
 - `git checkout -b <new-branch-name>`
 - `git push --set-upstream origin <new-branch-name>`
 - Now if you do `git branch -vv` you'll see that local branch is tracking the remote branch. 
 - run `git fetch -p`. After this remote branch is deleted (after merge) you'll see that `git branch -vv` mentions `gone` against the remote branch. This was you know that local branch is no longer useful and delete it. In the first option above, it is hard to find out whether a local branch has been delivered and not longer usefu. So it is hard to delete it for cleanup.
 
 
 
### create branch localy and push it to github
 
`git checkout -b 'feature-1'` - Create and switch to new branch
 
```
 git branch --set-upstream-to origin/feature-1
 git push 
```
Above sets remote tracking branch for current branch
 
 or you can do 
 
```
 git push origin feature-1:feature-1
``` 
 
 above will create a new branch on remote 'origin' and push changes of local branch to that branch

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
 
 
 
1. Look at `git branch -vv`
 
 Above will list all the branches with it's remote tracking branches. If you see the `gone` mentioned along side of the remote branch, that it may be a case were the branch was merged using a PR and then workflow has deleted the remote branch on GH. Local Branches where remote branches are `gone` can be deleted.
 
2. To further confirm whether the most lastest commit on the local branch have been added to main, you can search the main branch using command below for the commit message of the last commit on the local branch.
 
 `git log main --grep="fix: add missing README files`
 
 
#### How to completely remove local branch and remote-tracking branch and start fresh from remote branch:
 
 In case you have messy code in your local branch that you have committed but not pushed to remote. You want to get rid of this code and start afresh from remote branch. For this you have to 
 1) Delete local branch: `git branch -D file-sync-22-master-1623760119`. Check using `git branch -vv`
 2) Delete local remote-tracking branch: `git branch -dr origin/file-sync-22-master-1623760119`. Check using `git remote show <remote-name>`
 3) Get remote branch in local tracker branch again: `git pull`. Check using `git remote show <remote-name>`
 4) Create new local branch from newly created local remote-tracking branch: `git checkout -b file-sync-22-master-1623760119 origin/file-sync-22-master-1623760119`. Check using `git branch -vv`.
 
 `ref:` https://stackoverflow.com/a/23961231/2331225
 
 
 

### About git ignore:

- git ignore doesn't have a command. It is only controlled by patterns mentioned in the files.
- There are two files that you can edit. Below is except from [here](https://git-scm.com/docs/gitignore)
  ```
  Which file to place a pattern in depends on how the pattern is meant to be used.

  Patterns which should be version-controlled and distributed to other repositories
  via clone (i.e., files that all developers will want to ignore) should go into a .gitignore file.

  Patterns which are specific to a particular repository but which do not need to be shared with other
  related repositories (e.g., auxiliary files that live inside the repository but are specific to one
  user’s workflow) should go into the $GIT_DIR/info/exclude file.
  ```
  
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

### How to troubleshoot : 'Your branch and 'origin/master' have diverged' problem.

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

Now there are two solutions when you have to synch up two branches: rebase or merge.

In this case, we want to synch up with same branch on remote server. 
 
 Since merge creates a non-linear history, rebase is preferred by many. 
rebase essentially brings in commit5 from remote into your local repo and then puts back commit4 on top of that. 
 
To use this option :
 ```
git pull --rebase
```
 See the https://stackoverflow.com/questions/2452226/master-branch-and-origin-master-have-diverged-how-to-undiverge-branches/2452610
 
 
 
### synching your local feature branch with main (or some other branch)
 
 Here you have two options like in above case: rebase or merge
 
 In above case we were getting latest commits from remote of same branch, but in here, we want to get latest commits from main branch and make our branch latest.
 
 - If your feature branch is public (i.e pushed to github) then use merge as merge doesn't change SHA of existing commits but creates a new merge commit (to avoid this, many people use rebase as below)
 
   ```
 git switch main
 git pull
 git switch feature
 git merge main
 ```
 
 - if your feature branch is still only on your local then use rebase as rebase creates a linear history by getting commits from main to your branch (keeping the SHA same) and then recreating your commits on top of those (SHA changes for your commits). It is said `rebase feature onto main`
 
 ```
 git switch main
 git pull
 git switch feature
 git rebase main
 ```
 
 **REMEMBER: But rebase alters old commits and create new ones** so if the branch has been made public then **rebase should not be used**.

 - reference: https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing
 - [Golden rule of rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing)

How to remove files from 'Changes not staged for commit' category of git status :
```
git checkout <file>
```
git checkout essentially overwrites your local modified file by latest copy from local branch.


how do you know if you have committed changes in your local branch but not pushed to remote :
Run git status.  Message would say that 'your local is ahead of remote by x number of commits'

Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

This means you have one commit that you have not pushed. 

To see what is going to get committed in next push :
```
git log --stat
```

This will give you history of commits. From this history, you can see one commit that are marked with (head->master), and then few commits down the line, you'll see a commit marked with (origin/master, origin/HEAD). 
In the next push, your commit marked with (head->master) and all the commits till and not including (origin/master, origin/HEAD) will be pushed. 


Different file states in git :


- Unstaged : untracked files + modified tracked files
    ```
    git add
    ```
- Staged : files that are ready to go in next commit
    ```
    git commit
    ```

- Committed files to local branch
    ```
    git log --stat
    ```

- Pushed to remote repo
    ```
    git log --stat
    ```

Git file moving through various states :

- when you create a new file, it is untracked :


now make this a tracked file :







Now to change it back to untracked :







To untrack everything which is there in staging area :
```
git reset
```

How to remove files from 'Changes not staged for commit' category of git status :
```
git restore <file>
or
git checkout <file>
```

git checkout essentially overwrites your local modified file by latest copy from local branch.


add to the staging area :

modified of the already updated file, just for the completeness of the example :

to move back to previous state :

Now commit these files to local git branch :

see your commit in local branch log :

Now roll back commit which still in local brach and not pushed to shared repo :
```
git reset --soft HEAD~
``` 
( --mixed will undo the commit + it'll unstage the changes from staging area,  but will leave changes in the working copy as is.
--hard will undo the commit, unstage the changes and update the working copy with what is in the local branch)

Now push commit to remote repo 



First commit them back in :






see Git log to confirm what is going to get pushed :


















Now push to remote :





















check the git log of remote repo to see that the commit has been made :







Now undo commit from remote repo :
(ref: https://gist.github.com/gunjanpatel/18f9e4d1eb609597c50c2118e416e6a6)

first check if you are on the right branch by running git status. Then

```
git revert a81b684513aa2d3faa2cced70460797cc8397528
```
this will not rewrite the history unlike reset above

This can also be done using reset (not recommended as rewrites history) :
```
git reset a81b684513aa2d3faa2cced70460797cc8397528 --hard
```
(here commit number is the commit which you want to point to going foward. i.e all the commits after
this one will be removed from github, also from insights>network )

and then run :
```
git push origin main -f
```


storing your changes in a separate branch :

Suppose you are working on branch B1. You have made changes to certain files. You now think that these changes are not required for now and you want to store these changes as a separate branch and come back to B1 and start working on that. For example : I was working on a project where first I tried to integrate with RDBMS using JPA. All these changes were pushed to B1. Then I started to make changes on my local to integrate with DynamoDB instead of RDBMS. But that didn't go well. So, Now I wanted to go back to last commited changes on B1 without loosing my DynamoDB changes. So I decided that I'll create a new branch and store DynamoDB changes on a that branch. And then again switch back to B1 and continue working on RDBMS. Below is the sequence of commands that helped.
```
git branch NoSQL
git checkout NoSQL
```
now you'll see that master, NoSQL and origin/master are on the same commit using 'git log'

commit 009ed95a6d83e5b899b5c864a8b84bf72cbb4740 (HEAD -> NoSQL, origin/master, master)
```
git status

git add .

git commit -m 'Initial attempt at sing DynamoDB'

git push origin NoSQL

git checkout master
```
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

remember that when cherry picking, you don't have to mention the source-branch. Just mention the commit sha.

By default cherry pick will bring in the changes from source commit and commit them to your branch. See the command below. (you can use -n option if you don't want to commit the incoming changes. Then it'll just stage those changes, which you can edit and manually merge. This is very useful)
 
```
 $ git cherry-pick -S e43a6
Finished one cherry-pick.
[master]: created a0a41a9: "More friendly message when locking the index fails."
3 files changed, 17 insertions(+), 3 deletions(-)
```
 
 Or cherry pick a range of commits. Notice the `^` character at the end of first commit. This is to indicate to git to include that commit as well in cherry pick:
 
 ```
 git cherry-pick -S dc99f87656a952f3548c320c6459278876f9f7b7^..6967cfc4751c87579c563ba9cbb3721116b72be0
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
 
  ```
 git cherry-pick -S 2493781^..c5e9df3
 ```



 ### What to do when you have unsigned commits in your PR

  
 
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

### (not recommended) how to sign commits that you have already pushed to Github

#### Recommended
 
 - One way which is not recommended is to amend the commits and force push. But this will rewrite the history. So, not suggestable.
 - Second approach is to create a new branch, cherry-pick all commits of the old branch to new branch and sign them in the process
 - create a new PR for merging and close old PR without merging
 - Above steps in more details
 - go to intellij and switch to `main`
 - git pull
 - git branch new-branch
 - git switch new-branch
 - git cherry-pick -S 2493781^..c5e9df3 (here the first commit sha is taken from first commit of the old PR and the second sha is last commit)
 - push this branch and create a new PR
 - close old PR
 
#### Not recommended (uses force push) 
 
 Reference: https://stackoverflow.com/questions/13043357/git-sign-off-previous-commits
 
 Remember that commit number will change when you do this. So, you'll have to force push to github.
 
 `git rebase --signoff -S HEAD~3` : this will add PGP sign and `signed-off by` message to last three commits
 
 `git rebase --signoff -S <SHA>` : this is for one particular commit 
 
 after this do `git push --force-with-lease` to push out changes. But one thing that I noticed is that in the PR I could still see previous unsigned commits. I expected those commits to be overwritten.
 
 
 ### why to avoid force push 
 https://blog.developer.atlassian.com/force-with-lease/
 
### git revert
 
### git clean 

remove all the untracked files from repo
 
```
git clean -f
```

remove all untracked, ignored files plus directories. 

```
git clean -dxf
```

### rewriting a commit message
 
 Commit message is part of commit itself, so when you change the message, the commit sha changes. It is like you are creating new commit and replacing old one. 
 
 - if commit has not been pushed: `git commit --amend`
 - If commit has been pushed to remote(GH): Since old commit has already been pushed, you'll have to force push new commit which is a bad practise. So, in this case, you better create a new branch and new PR with good commit. Close the old PR without merging.
 Reference: https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/changing-a-commit-message
 
 ### check commit signatures 
 
 ```
 git log --show-signature
 ```

 ### How to create commit without any code change (empty commit)
 
 ```
 git commit --allow-empty -S -m 'docs: no changes required'
 ```

 ### Stash
 
 To stash whatever you have now (tracked + untracked)
 
 ```
 git stash push -u -m 'my stash message'
 ```
 
 To get the last stash reapplied (`--index` will stage the files again which were previously staged)
 
 ```
 git stash apply --index
 ```
 
 List all awailable stashes:
 
 ```
 git stash list
 ```
 
 See contents of a particular stash:
 
 ```
 git stash show stash@{0}
 ```
 
 Delete or drop a stash
 
 ```
 git stash drop stash@{0}
 ```
 
 Apply stash by name
 
 ```
 git stash apply stash^{/my_stash_name}
 ```
 
 ### apply signature to commit automatically
 
 Use below command as one-time setting 
 
 ```
 git config --global commit.gpgsign true
 ```
 
 Due to this
 - all commits will be signed automatically, like what `git commit -S` command does manually. You can ignore `-S` now
 - if you cherry-pick a commit, all commits are newly created. In this case, commits will be auto signed
 - if you `rebase` any thing, all commits are newly created. In this case, commits will be auto signed

### mentioning someone else as author in a commit
 
 ```
 git commit --author="temp-ossdhaval" -S -m 'message'
 ```

 ### difference between GPG sign a commit (-S) vs adding Sign-off (-s)
 
 - GPG signing is done by adding -S to commit command. Using this GH can verifies only the intended dev is making the commit.
 - `sign off by` is added by `-s`. It is up to the organisation how to interprete the sign off given by the developer.
 - in intellij you can configure signing of every commit with gpg using alt+ctrl+s -> search git -> click configure GPG -> check mark on `sign all commits`
 - sign-off can be done by clicking `commit options` on the commit tool window that can open using `ctrl+0`

 ### Detached head state
 
 - HEAD is a file in git that points to the current branch normally
 - sometimes HEAD can also contain a SHA value of a commit. This is `detached HEAD` state. This happens when you checkout a particular commit, a tag, a PR, or a remote branch without fetching it first. 
  
 ### Branch vs Tag
 
 - Branch is a reference to a commit and that reference changes when next commit is made
 - Tag is also a reference to a commit and it will **not** move if new commits are made

 ### How to know if there are any conflicts between two branches
 
 - Before raising a PR for your feature branch, if you want to know if PR will get merge conflict with base branch(let's say main) or not, then do this locally on your system:
 
 ```
 # make sure you are on feature branch
 git swith feature-branch
 
 # create temp branch from your feature branch
 git checkout -b temp-feature-branch
 
 # merge main
 git merge main
 
 # this will give you output as below. It'll exactly tell you if there are conflicts and which files
 Auto-merging docs/admin/auth-server/crypto/key-generation.md
 CONFLICT (content): Merge conflict in docs/admin/auth-server/crypto/key-generation.md
 Automatic merge failed; fix conflicts and then commit the result.
 
 # abort the merge
 git merge --abort
 
 # Now since our purpose is served, Delete the temp branch 
 git switch feature-branch
 git branch -D temp-feature-branch

 # Working with patch

 Git doesn't have a `git patch` command. What it has is `git format-patch` command. 

 ## Create a patch

 Of uncommitted changes
 ```
git diff > my_patch.diff
```

Generate a Patch for Staged Changes
```
git diff --cached > my_patch.diff
```

 Generate a Patch for the Last Commit
 ```
git format-patch -1
```

## Apply a patch

apply a patch file
```
git apply my_patch.diff
```



 
