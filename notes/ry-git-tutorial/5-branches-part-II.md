# Branches Part II

- it's useful to assign special meaning to different branches
  for example, `master` are stable branch
  `css` branch are temporary branch we called `topic branch`
  because they exist to develop a certain `topic`, then they are deleted

- some merges cannot be `fast-forward`
  when the history of two branches diverges, a dedicated commit is required to combine the branches
  this situation may also give rise to a `merge conflict`

## Continue the Crazy Experiment

- the `crazy` branch is a longer-running type of topic branch called a `feature branch`
  as it was created with the intention of developing a specific `feature`
  `feature branch` enable you focus on developing one clearly defined `feature`

- create a new branch for each major addition to your project
- don't create a branch if you can't give it a specific name.

## merge the CSS updates

- `git merge master`

- `3-way merge`
  a 3-way merge occurs when you try to merge two branches whose history has diverged.
  it creates an extra `merge commit`
  it has `two` parent commits
  it's like saying `this commit comes from both the crazy branch and from master`

## Emergency Update

- `hotfix branch`
  hotfix branch are used to quickly patch a production release.

```
git checkout master
git branch news-hotfix
git checkout news-hotfix
```

- `git commit -a -m "xxx"`
  `-a` auto include `all tracked` files in the staged snapshot

## publish the News Hotfix

```
$ git checkout master
$ git merge news-hotfix
$ git branch -d news-hotfix
```

## Merge Conflict

```
<<<<<<<<<<HEAD
111
=============
222
>>>>>>>>>>> crazy
```

- the `<<<<<<HEAD` shows us the version in the current branch
  while the `==========` shows the version in the `crazy` branch

- the `<<<<`, `====`, `>>>>` markers are only used to show us the conflict and should be deleted

- next we need to tell Git that we're done resolving the conflict with `git add` command

- `git commit`
  we didn't use the `-m` flag, because Git gives us a default message for merge commits

## cleanup the Feature Branches

```
$ git branch -d crazy
$ git branch -D crazy-alt // force delete
```
