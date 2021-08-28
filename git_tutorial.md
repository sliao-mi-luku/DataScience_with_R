# Git Tutorial

Resrource:
Udacity, Programming for Data Science in R Nanodegree

### create a repo
```
$ git init
```

### clone
```
$ git clone <link_of_the_existing_repo>
$ git clone <link_of_the_existing_repo> <name_of_the_clone_repo>
```

### check status
```
$ git status
```

### git log
Display the information about the **existing commits**
```
$ git log
$ git log --oneline   # display each commit in 1 line
$ git log --stat      # display what (how many) files changed and how many lines changed
$ git log -p          # display the changes made
$ git log -p -w       # ignore whitespace changes
$ git log -p <SHA>    # display starting at the specified <SHA>

$ git log --oneline --graph --all     # display all commits from all branches
```

### git show
Display information about the **given commit**
```
$ git show                # display the most recent commit
$ git show <SHA>          # display the specific commit
$ git show <SHA> -p
$ git show <SHA> --stat
```

### git add
Add the files from the working directory **to the staging index**.
- It's helpful to track the status by `$ git status` after any move.
```
$ git add <filename>                               # stage 1 file
$ git add <filename1> <filename2> <filename3>      # stage 3 files
$ git add .                                        # stage all contents in the directory
```
If a wrong file is added to the staging index, undo it by:
```
$ git rm --cached <filename>
```

### git commit
Take the files from the staging index and save them in the repository
```
$ git commit
$ git commit -m "Initial commit"       # avoid the editor step
```

### git diff
Display the changes that have been made but not committed yet
```
$ git diff
```
### Ignore files
If you want git to ignore some files, you can create a file named `.gitignore` and put the filenames that you want to be ignored into `.gitignore`.

Use globbing to specify multiple files. For example" `images/*.jpg`

### git tag
Add tags to specific commits
```
$ git tag v1.0              # create a lightweight tag to the most recent commit
$ git tag -a v1.0           # create an annotated tag to the most recent commit (recommended)
$ git tag -a v1.0 <SHA>     # create an annotated tag to the specified commit
$ git tag -d v1.0           # remove an existing tag
$ git tag                   # display all tags in the repo
```
The location where the tags were attached can be seen by `$ git log`

### git branch
Allow multiple lines of development
```
$ git branch                # list all branches in the repo (the active branch will be marked by *)
$ git branch <NAME>         # create a branch named <NAME>
$ git branch <NAME> <SHA>   # create a branch named <NAME> and have it point to the commit <SHA>
$ git branch -d <NAME>      # delete the branch named <NAME>
$ git branch -D <NAME>      # force deletion of the branch named <NAME> that contains some unique commits
```

### git checkout
Switch between different branches and tags
```
$ git checkout <NAME>                 # switch to the branch named <NAME>
$ git checkout -b <NAME>              # create a new branch called <NAME> and switch to there
$ git checkout -b <B_NEW> <B_REF>     # create a new branch called <B_NEW> at the same location as an existing branch <B_REF>
```

### git merge
Merge another branch to the current (active) branch
```
$ git merge <B_NAME>                 # merge the <B_NAME> branch to the active branch
```
If a merge conflict happens:
1. locate *ALL* conflict indicators
2. choose which one to keep (I found Atom has this function)
3. save the file
4. stage the file
5. make a commit

### git commit --amend
Alter the most recent commit
```
$ git commit --amend
```
Using the commend directly after a commit can enable you to re-edit the commit messages.

To amend files that you just recently committed:
1. edit the files
2. save the files
3. stage the files
4. run `$ git commit --amend`

### git revert
Reverse a specific commit
```
$ git revert <SHA>        # revert the <SHA> commit
```
Reverting a commit will create a new commit

### Relative commit references
`^` indicates the  **first** parent commit (the branch you were on when you run merging)
`^2` indicates the  **second** parent commit (the branch you called to merged)
`~` indicates the **first** parent commit


The parent commit: `HEAD^`, `HEAD~`, or `HEAD~1`

The grandparent commit: `HEAD^^` or `HEAD~2`

The great-grandparent commit: `HEAD^^^` or `HEAD~3`

### git reset
Delete commits (dangerous). The new location of the HEAD is given by relative commit references (see above).
```
# assume that we are at HEAD -> <SHA>
$ git reset HEAD~1             # move the HEAD to HEAD~1, <SHA> will be moved to the working directory
$ git reset --mixed HEAD~1     # move the HEAD to HEAD~1, <SHA> will be moved to the working directory
$ git reset --soft HEAD~1      # move the HEAD to HEAD~1, <SHA> will be moved to the staging index
$ git reset --hard HEAD~1      # move the HEAD to HEAD~1, <SHA> will be moved to trash
```

### git reflog
Access the commits that you deleted within 30 days.

### git remote
Manage remote repository
```
$ git remote                      # display the remote repo you cloned
$ git remove -v                   # display the full path to the remote repo
$ git remote add origin <URL>     # create the connection from the local repo to a remote repo
```

### git push
Send changes to the remote repository
```
$ git push origin <BRANCH_NAME>   # push <BRANCH_NAME> to a remote repo (whose shortname is origin)
```

### git pull
Retrieve updates from the remote repository
```
$ git pull origin <BRANCH_NAME>   # pull a remote repo (whose shortname is origin) and merge to <BRANCH_NAME>
```

### git fetch
Retrieve commites from the remote repository but without merging with the local branch
```
$ git fetch origin master        # pull origin to the local repo, the most recent commit retrieved will be pointed by origin/master
$ git merge origin/master        # merge origin/master with master
```

### git shortlog
See how many commits each contributor has added
```
$ cd <repo_directory>
$ git shortlog
$ git short log       # just show the number and sort numerically
```

### search commits by contributors
```
$ git log --author=Sam           # see commits by a specific contributor
$ git log --grep="bad bugs"      # filter commits that have the word "bad bugs"
```

