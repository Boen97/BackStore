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
