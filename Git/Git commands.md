[Git info](https://www.atlassian.com/git/tutorials/setting-up-a-repository)
https://youtu.be/XuFaQSW79rM

**git clone**
`git clone <repo> <directory>`

**git status**
`git status`
List which files are staged, unstaged, and untracked.

**git add** + **git commit**
The `git add` command adds a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit.
```
git add .
git commit
```
Once you’ve got your project up-and-running, new files can be added by passing the path:
```
git add hello.py
git commit
```
The `git reset` command is used to undo a `git add`

**git restore**
The `git restore` command is used to *undo uncommitted changes* in your working directory or staging area
```
git restore --staged .
```

**git push**
`git push <remote> <branch>`
Push the specified branch to , along with all of the necessary commits and internal objects. This creates a local branch in the destination repository.

**git pull**
`git pull <remote>`
Fetch the specified remote’s copy of the current branch and immediately merge it into the local copy. This is the same as `git fetch ＜remote＞`

**git branch**
`git branch`
List all of the branches in your repository. This is synonymous with `git branch --list`
`git branch <branch>`
Create a new branch called *branch*. This does not check out the new branch.
`git branch -d <branch>`
Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has unmerged changes.
`git branch -D <branch>`
Force delete the specified branch, even if it has unmerged changes. This is the command to use if you want to permanently throw away all of the commits associated with a particular line of development.
`git branch -m <branch>`
Rename the current branch to branch.
`git branch -a`
List all remote branches.

**git checkout**
The `git checkout` command lets you navigate between the branches created by `git branch`

Example:
```
$＞ git branch 
main 
another_branch 
feature_inprogress_branch 
$＞ git checkout feature_inprogress_branch
```

`git checkout -b ＜new-branch＞`
Command accepts a *-b* argument that acts as a convenience method which will create the new branch and immediately switch to it

**git fetch**
`git fetch <remote>`
Fetch (Извлечь) all of the branches from the repository. This also downloads all of the required commits and files from the other repository.
`git fetch <remote> <branch>`
Fetch the specified branch.

**git rebase**
`git rebase <base>`
This automatically rebases the current branch onto `＜base＞`.

**git merge**
`git merge <branch>`
Will combine multiple sequences of commits into one unified history. In the most frequent use cases, `git merge` is used to combine two branches.

**merge** - оставляет историю (больше коммитов, после merge - новый коммит слияния в основной ветке, другая продолжает существовать и не зависит от основной)
**rebase** - переписывает историю (меньше коммитов, после rebase последний коммит перезаписывается и остаётся основным. Ветка, которая была родительской - удаляется).

**git log**
`git log --oneline`
It displays only the commit ID and the first line of the commit message.

Output example:
```
0e25143 Merge branch 'feature'
ad8621a Fix a bug in the feature
16b36c6 Add a new feature
23ad9ad Add the initial code base
```

**git revert**
`git revert <id>`
Creates a new commit with the changes that are rolled back.

**git reset**
`git reset <id>` 
Erases your Git history after commit instead of making a new commit.

**git stash**
`git stash` temporarily shelves (or _stashes_) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later on.