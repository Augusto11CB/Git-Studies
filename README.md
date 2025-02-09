# Git-Studies

## To Study
[Git Hooks](https://www.atlassian.com/git/tutorials/git-hooks)
[Git Cherry Pick](https://www.atlassian.com/git/tutorials/cherry-pick)

## Index
TODO

## How to Delete Branch Locally and Remotely
```
$ git push -d <remote_name> <branch_name>
$ git branch -d <branch_name>
```

Note that in most cases the remote name is origin. In such a case you'll have to use the command like so.

```
$ git push -d origin <branch_name>
```

## Git Log Useful Commands

### Cloning git repository when folder and files already exist


```
git init
git remote add origin <my-github-rep.git>
git fetch
git branch --set-upstream-to=origin/master
```

### List of remotes for a Git repository?
```
$ git remote
iqandreas
octopress
origin
```

### Showing one commit per line
`$ git log --oneline`

### The `--stat` 
Flag that can be used to display the files that have been changed in the commit, as well as the number of lines that have been added or deleted.
`$ git log --stat`

### How to see changes in a file?
This flag can be used to display the actual changes made to a file.
`$ git log -p`


## Push an existing repository from the command line
`$ git remote add origin git@github.com:AugustoCalado/Test-Repo.git`

`$ git push -u origin master`

## How to change the remote a branch is tracking?
`$ git branch branch_name -u your_new_remote/branch_name`

## How to solve git refusing to merge unrelated histories on rebase?

`$ git pull origin master --allow-unrelated-histories`

`$ git merge origin origin/master`

... add and commit here...

`$ git push origin master`

## The git stash 
Use git stash when you want to record the current state of the working directory and the index, but want to go back to a clean working directory. 

### The git stash -p 
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

### Stage specific files
`$ git stash push -m stash_name example/file/path/and/file.html`

### The git stash branch <branch_name> [<stashnumber>]
Creates and checks out a new branch named <branchname> starting from the commit at which the <stash> was originally created, applies the changes recorded in <stash> to the new working tree. It then drops the stash. 
   
### Show files inside a stash
`$ git stash show -p stash@{x}`

#### Show only the files name inside a stash
`$ git stash list --name-status`

### How can to git stash a specific file?
`$ git stash push -m welcome_cart app/views/cart/filename.ext`

## Push Existing Repo to a New and Different Remote Repo Server?

```
$ git remote add github-repo <github-repo-url>
$ git checkout master
$ git push github-repo master    # push current-repo master branch changes to github-repo master branch

$ git remote #shows the remotes tracked
```

## How to rename Git Local and Remote Branches

1. Rename Local Branch

`$ git branch -m new-name`

   * If i am on a different branch
   
   `$ git branch -m old-name new-name`
   
2. Delete the old-name remote branch and PUSH the new-name local branch

`$ git push origin :old-name new-name`

3. Reset upstream branch for the new

`$ git push origin -u ne-name`


## Create Branch from a Previous commit

`$ git branch branchname <sha1-of-commit>`

using a symbolic reference:

`$ git branch branchname HEAD~3`

To checkout the branch when creating it, use:

`$ git checkout -b branchname <sha1-of-commit or HEAD~3>`

## How Can I Determine the Url That a Local Git Repository Was Originally Cloned From?
`$ git remote get-url origin`

`$ git remote -v`

`$ git remote show origin`

## How to change repo cloned using https to ssh?

1. remove HTTP remote (for example with origin):
```
git remote remove origin
```

2. add the SSH remote
```
git remote add origin user@example.com:path/to/project.git
```

3. set the branch's remote again with
```
git push -u origin master

or

git branch --set-upstream-to=origin master
```

## How to Untrack Files Already Added to Git Repository Based on .gitignore
1. Commit all changes

2. Remove everything from the repository

`$ git rm -r --cached .`

   - rm is the remove command

   - `-r` will allow recursive removal

   - `–cached` will only remove files from the index.

3. Re add everything

`$ git add .`

4. Commit

`git commit -m ".gitignore fix"`

## How to Correct a Commit Date
Rebase to the commit immediately prior to the commit with the wrong date

`$ git rebase <commit hash> -i`


Result:
```
pick af09d0a Log and add new dependency   # Commit with wrong date

pick 4e37143 exchanging stop by timeout for buffersize

pick 21fc337 Added simple styles in home.html

pick 8dc79f6 create readme             
```

Replace pick with e (edit) on the line with that commit (the first one)
```
e af09d0a Log and add new dependency   # Commit with wrong date

pick 4e37143 exchanging stop by timeout for buffersize

pick 21fc337 Added simple styles in home.html

pick 8dc79f6 create readme             
```

Adjust the commit date with 
`$ git commit --amend --no-edit --date "6 Apr 2018"`


to change the commit date instead of the author date:

`GIT_COMMITTER_DATE="Wed Feb 16 14:00 2011 +0100" git commit --amend`


```
GIT_COMMITTER_DATE="Mon 20 Aug 2018 20:19:19 BST" git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 BST"
```


Finish by typing the follow command
`$ git rebase --continue`

[RFC 2822 Formater](https://timestampgenerator.com/1604371652/-03:00)
   
## Creating tags from the command line
To create a tag on your current branch, run this:

git tag <tagname>
### Include a Description with a Tag
- `$ git tag <tagname> -a`

### Push Tags to Remote Repo
- `$ git push origin --tags`

### Push a Single Tag to Remote Repo
- `$ git push origin <tag>`

### To Delete Local Tag
- `$ git tag -d <tag>`
- `$ git push origin :refs/tags/<tag>`
   
## References
[merging-vs-rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
[Resetting, Checking Out & Reverting](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting)
[Advanced Git Log](https://www.atlassian.com/git/tutorials/git-log)
[Merge Strategy](https://www.atlassian.com/git/tutorials/using-branches/merge-strategy)
