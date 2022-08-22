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
