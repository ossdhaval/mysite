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