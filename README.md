# Git-Studies

## Index
TODO

## git stash 
Use git stash when you want to record the current state of the working directory and the index, but want to go back to a clean working directory. 

### git stash -p 
This command will then show a dialog like the following, for every hunk in your possible commit
`Stash this hunk [y,n,q,a,d,e,?]?`

#### Meaning of the letters
```
   y - stage this hunk
           n - do not stage this hunk
           q - quit; do not stage this hunk nor any of the remaining ones
           a - stage this hunk and all later hunks in the file
           d - do not stage this hunk nor any of the later hunks in the file
           g - select a hunk to go to
           / - search for a hunk matching the given regex
           j - leave this hunk undecided, see next undecided hunk
           J - leave this hunk undecided, see next hunk
           k - leave this hunk undecided, see previous undecided hunk
           K - leave this hunk undecided, see previous hunk
           s - split the current hunk into smaller hunks
           e - manually edit the current hunk
           ? - print help
```

A hunk is a coherent diff of lines as git-diff produces it. To select a single file you'll have to decline adding hunks as long as you reach that file, then you might add all hunks from that file.

**Observation**
Using the --patch-option is possible on different git commands (f.e. stash, commit and add).

### Stage the specific files
`git stash push -- example/file/path/and/file.html`

### git stash branch <branch_name> [<stashnumber>]
Creates and checks out a new branch named <branchname> starting from the commit at which the <stash> was originally created, applies the changes recorded in <stash> to the new working tree. It then drops the stash. 
   
### Show files inside a stash
`git stash show -p stash@{x}`

#### Show only the files name inside a stash
`git stash list --name-status`

## Push Existing Repo to a New and Different Remote Repo Server?

```
$ git remote add github-repo <github-repo-url>
$ git checkout master
$ git push github-repo master    # push current-repo master branch changes to github-repo master branch

$ git remote #shows the remotes tracked
```

## How to rename Git Local and Remote Branches

1. Rename Local Branch
> git branch -m new-name
   * If i am on a different branch
   > git branch -m old-name new-name
2. Delete the old-name remote branch and PUSH the new-name local branch
> git push origin :old-name new-name

3. Reset upstream branch for the new
> git push origin -u ne-name


## Create Branch from a Previous commit

> git branch branchname <sha1-of-commit>

using a symbolic reference:
> git branch branchname HEAD~3

To checkout the branch when creating it, use:
> git checkout -b branchname <sha1-of-commit or HEAD~3>
