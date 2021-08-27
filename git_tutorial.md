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

###
