# Rewriting history

we'll learn how to split up commits, revive snapshots, and completely rewrite a repository's history to our exact specifications

- `git checkout -b new-pages`
  created a new branch and checked it out

## fix bad commit

- rules:
1. commit a snapshot for each significant addition to your project.
2. don't commit a snapshot if you can't come up with a single, specific message for it.

this will ensure that your project has a meaningful history

however, in practice, you'll often wind up `committing several` changes in a single snapshot

we want to imporve these commits

```
4c3027c Add green page
db96c72 Add new HTML pages
```

to

```
4c3027c Add green page
9b1a64f Add yellow page
77a1cf1 Add red page
```

### begin an Interactive Rebase

```
$ git rebase -i master

edit db96c72 Add new HTML pages
pick 4c3027c Add green page
```

### Undo the Generic Commit

```
$ git reset --mixed HEAD~1
```

- the `git reset` command moves the checked out snapshot to a new commit
- the `HEAD~1` tells it to reset to the commit that occurs before the current HEAD
- `HEAD~2` woudl refer to second commit before `HEAD`

- `git reset --hard`
- `--hard` flag told Git to make the working directory look exactly like the most recent commit
- `--mixed` flag preserve the working directory, which contains the changes we want to seprate
- that is the `HEAD` moved, but the working directory remained unchanged.

```
$ git add red
$ git commit -m "add red"

$ git add yellow
$ git commit -m "add yellow"
```

then `git rebase --continue` to finish the rebase

## Remove the Last Commit

```
$ git reset --hard HEAD~1
```

- `dangling commit` are those that cannot be reached from any branch

## open the Reflog

Git uses `reflog` to record every change you make to your repository

- `git reflog`

the reflog is a `chronological listing` of our history, without regard for the repository's branch structure
this lets us find `dangling commits` that would otherwise be lost from the the project history

## Revive the Lost Commit

at the beginning of each `reflog entry`, you'll find a commit ID representing the `HEAD` after that action
check out the commit at `HEAD@{2}`

```
$ git checkout 1f7ed37
```

this puts us in a `detached HEAD` state, which means our `HEAD` is no longer on the tip of a branch

now we're looking at a commit `after` the tip of the branch, but we still a `detached HEAD`

to turn out `dangling commit` into a full-fledged branch, we have to create one.
`git checkout -b green-page`
we now have a branch that can be merged back into the project.

### Filter the Log History

to view the differences between branches, we can use Git's `log-filtering` syntax.
`git log new-pages..green-page`
this will display all commits contained in `green-page` that aren't in the `new-pages` branch

`git log HEAD~4..HEAD` limit the output of `git log`
`git log -n 4` only show the last four commits

### Merge in the Revived Branch

```
$ git checkout master
```

`git log HEAD..green-page --stat`

- `--stat` includes information about which files have been changed in each commit

`git merge green-page`

## Conclusion

- Git uses the tip of a branch to represent the `entire branch`
- that is a branch is actually a pointer to a single commit-not a container for a series of commits
- the `history` is represented by the parent of each commit
