# Git

Resrource:
Udacity, Programming for Data Science in R Nanodegree

### create a repo

```terminal
$ git init
```

### clone

```terminal
$ git clone <link_of_the_existing_repo> <name_of_the_clone_repo>
```

### check status

```termimnal
$ git status
```

### git log

Display the information about the existing commits
```terminal
$ git log
```

Show each commits by a single line:
``` terminal
$ git log --oneline
```

Have a closer look at what file has changed, or how many lines were added/deleted:
``` terminal
$ git log --stat
```

Display acutal changes:
```terminal
$ git log -p

$ git log --patch
```

### git show

Display information about the given commit
```terminal
$ git show <SHA> -p

$ git show <SHA> --stat
```

Display information of the most recent commit
```terminal
$ git show
```

### git add

Add the files from the working directory to the staging index.

It's helpful to track the status by `$ git status` after any move.

```terminal
$ git add index.html
$ git status
```
If a wrong file is added to the staging index, undo it by

```terminal
$ git rm --cached index.html
```

To stage all contents in a directory

```terminal
$ git add .
```

### git commit

```terminal
$ git commit

# to avoid the editor step
$ git commit -m "Initial commit"
```




