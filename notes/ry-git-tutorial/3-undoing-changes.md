# Undoing Changes

storing `safe` versions isn't much help without the ability to restore them.

how to view the previous states of a project, revert back to them, and reset uncommitted changes.

## View an Old Revision

```
$ git log --oneline

c711307 (HEAD -> master) modify test2.txt
4db38de add test2.txt
687a130 add test1.txt
```

```
$ git checkout 4db38de
$ git log

4db38de (HEAD) add test2.txt
687a130 add test1.txt
```

```
$ git status

HEAD detached at 4db38de
```

all of our actions with previous commites took place on the `master` branch
to retrieve our complete history, we just have to checkout out this branch.

## return to current version

- `git checkout master`
  this makes Git update our working directory to reflect the state of the `master` branch's snapshot

## Tag a Release

- `git tag -a v1.0 -m "stable version 1"`
- the `-a` flag tell Git to create an `annotated tag`, which let us record our name, the date, and a descriptive message

## Undo committed Changes

```
$ git log --oneline

c612088 (HEAD -> master) crazy experiment
c711307 (tag: v1.0) modify test2.txt
4db38de add test2.txt
687a130 add test1.txt
```

```
$ git revert c612088
$ git log --oneline

3cebb4d (HEAD -> master) Revert "crazy experiment"
c612088 crazy experiment
c711307 (tag: v1.0) modify test2.txt
4db38de add test2.txt
687a130 add test1.txt
```

- when using `git revert`, remmber to sepecify the commit that want to undo-not the stable commit that you want to return to
- think of this revert commit as saying `undo this commit` rather than `restore this revision`

## Undo Uncommitted Changes

support we have a `tracked and modified` change in `test1.txt` and `test2.txt`, and a new untracked file `test3.txt`

- `git reset`
  unstage all tracked files, but keep the modifys in your working directory

- `git reset --hard`
  update the modified tracked files to the most recent commit
  `--hard` is what actually updates the file

- `git reset` only operates on the working directory and the staging area

- `git clean -f` remove all untracked files

> be careful with `git reset` and `git clean` both operate on the working directory
> not on the committed snapshots, they `permanently undo changes`
