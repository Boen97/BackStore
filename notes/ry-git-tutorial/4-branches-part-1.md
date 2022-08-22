# Branches, Part I

- components of Git version control

1. the working directory
2. the staged snapshot
3. the committed snapshots
4. development branches

- in Git, a `branch` is an independent line of development

## View Existing Branches

```
$ git branch

* master
```

the `master` branch is Git's default branch
the `*` next to it tells us that it's currently checked out.
this means that most recent snapshot in the `master` branch resides in the working directory

## checkout the crazy experiment

- `HEAD` is Git's internal way of indicating the snapshot that is currently checkout out.

```
$ git log --oneline

3cebb4d (HEAD -> master) Revert "crazy experiment"
c612088 crazy experiment
c711307 (tag: v1.0) modify test2.txt
4db38de add test2.txt
687a130 add test1.txt

$ git checkout c612088
```

## create a branch

- we can't add new commits when we're not on a branch, so let's create one now.

```
$ git branch crazy
$ git branch

* (HEAD detached at c612088)
  crazy
  master
```

- `git branch crazy` just creates a branch named `crazy`, it doesn't check it out.

## develop in crazy branch

```
$ git checkout crazy

modify test1.txt

$ git add test1.txt
$ git commit -m "modify test1.txt"
```

- `git log` only displays the history of the current branch
- `HEAD` automatically moved forward to the new commit

## rename file in crazy branch

```
git rm test1.txt
git add test11.txt
git commit -m "rename test1.txt to test11.txt"
```

- `git rm` tells Git to `stop tracking test1.txt`, and delete it if neccessary
- the git is smart enought to figure out the file rename

```
$ git log --oneline

0319059 (HEAD -> crazy) rename test1.txt to test11.txt
722004a modify crazy
c612088 crazy experiment
c711307 (tag: v1.0) modify test2.txt
4db38de add test2.txt
687a130 add test1.txt
```

## return to the master branch

```
$ git checkout master
$ git branch
```

- different branches are separate projects, just like different project folders
