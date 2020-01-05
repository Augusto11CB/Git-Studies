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


## Push Existing Repo to a New and Different Remote Repo Server?

```
$ git remote add github-repo <github-repo-url>
$ git checkout master
$ git push github-repo master    # push current-repo master branch changes to github-repo master branch

$ git remote #shows the remotes tracked
```

