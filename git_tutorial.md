# Git Tutorial

Resrource:
Udacity, Programming for Data Science in R Nanodegree

### create a repo
```terminal
$ git init
```

### clone
```terminal
$ git clone <link_of_the_existing_repo>
$ git clone <link_of_the_existing_repo> <name_of_the_clone_repo>
```

### check status
```termimnal
$ git status
```

### git log
Display the information about the **existing commits**
```terminal
$ git log
$ git log --oneline   # display each commit in 1 line
$ git log --stat      # display what (how many) files changed and how many lines changed
$ git log -p          # display the changes made
$ git log -p -w       # ignore whitespace changes
$ git log -p <SHA>    # display starting at the specified <SHA>
```

### git show
Display information about the **given commit**
```terminal
$ git show                # display the most recent commit
$ git show <SHA>          # display the specific commit
$ git show <SHA> -p
$ git show <SHA> --stat
```

### git add
Add the files from the working directory **to the staging index**.
- It's helpful to track the status by `$ git status` after any move.
```terminal
$ git add <filename>                               # stage 1 file
$ git add <filename1> <filename2> <filename3>      # stage 3 files
$ git add .                                        # stage all contents in the directory
```
If a wrong file is added to the staging index, undo it by:
```terminal
$ git rm --cached <filename>
```

### git commit

Take the files from the staging index and save them in the repository

```terminal
$ git commit

# to avoid the editor step
$ git commit -m "Initial commit"
```




