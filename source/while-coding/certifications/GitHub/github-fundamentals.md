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

Working tree: The set of nested directories and files that contain the project that's being worked on.

Repository (repo): The directory, located at the top level of a working tree, where Git keeps all the history and metadata for a project. Repositories are almost always referred to as repos. A bare repository is one that isn't part of a working tree; it's used for sharing or backup. A bare repo is usually a directory with a name that ends in .git—for example, project.git.

Hash: A number produced by a hash function that represents the contents of a file or another object as a fixed number of digits. Git uses hashes that are 160 bits long. One advantage to using hashes is that Git can tell whether a file has changed by hashing its contents and comparing the result to the previous hash. If the file time-and-date stamp is changed, but the file hash isn’t changed, Git knows the file contents aren’t changed.

Object: A Git repo contains four types of objects, each uniquely identified by an SHA-1 hash. A blob object contains an ordinary file. A tree object represents a directory; it contains names, hashes, and permissions. A commit object represents a specific version of the working tree. A tag is a name attached to a commit.

Commit: When used as a verb, commit means to make a commit object. This action takes its name from commits to a database. It means you are committing the changes you have made so that others can eventually see them, too.

Branch: A branch is a named series of linked commits. The most recent commit on a branch is called the head. The default branch, which is created when you initialize a repository, is called main, often named master in Git. The head of the current branch is named HEAD. Branches are an incredibly useful feature of Git because they allow developers to work independently (or together) in branches and later merge their changes into the default branch.

Remote: A remote is a named reference to another Git repository. When you create a repo, Git creates a remote named origin that is the default remote for push and pull operations.

Commands, subcommands, and options: Git operations are performed by using commands like git push and git pull. git is the command, and push or pull is the subcommand. The subcommand specifies the operation you want Git to perform. Commands frequently are accompanied by options, which use hyphens (-) or double hyphens (--). For example, git reset --hard.
