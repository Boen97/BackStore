# Rebasing

- Git includes a tool to help us `clean up our commits`, `git rebase`

> Rebasing lets us move branches around by changing the commit that they are `based on`

such as, you can rebase a feature branch onto master
after rebasing, the `feature branch` has a new parent commit, which is the same commit pointed to by `master`

`rebasing` integrates the `feature` branch by building on `top of master`
the result is a perfectly `linear history` that reads more like a story

## rebase the about branch

```
git checkout about
git rebase master
git log --oneline
```

- `git rebase` requires you to be on the branch that you want to move.

> `Rebasing` also allowed us to integrate the most up-to-date version of `master` without a `merge commit`

## cleanup up the commit history

before we merge into the `master` branch, we should make sure to have a `clean, meaningful history` in out feature branch
by `rebasing interactively`, we can choose `how each commit is transferred to the new base`

- `git rebase -i master`

interative rebasing can be dangerous, for example, if you were to delete a line from the rebase listing
the associated commit wouldn't  be transferred to the new base, and its content would be lost forever

## stop to Amend a Commit

we can `alter a snapshot during the rebase`

- `git commit --amend`
  `replace` the existing commit with the staged snapshot instread of creating a new one.

```
$ git rebase -i master

pick 58dec2a Create the about page
edit 6ac8a9f Begin creating bio pages
pick 51c958c Add link to about section in home page

git add about/mary.html
git status
git commit --amend
```

## continue the interactive rebase

- `git rebase --continue`
- `git log --oneline`

- `git rebase --abort` flag to abandon it

if you ever find yourself lost in the middle of a rebase and you're afraid to continue
you can use the `--abort` flag to abandon it and start over from scratch
