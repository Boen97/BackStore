# Remotes

a `remote repository` is one that is not your own.
`remote branch` act just like the local branches that we've been using, only they represent a branch in someone else's repository

```
git clone my-git-repo marys-repo
```

## config the repository (Mary)

```
$git config user.name "Mary"
$git config user.email mary@gmail.com
```

## Mary Work

```
$ git checkout -b bio-page
do some work...
$ git commit -a -m "Add bio page for Mary"

$ git checkout master
$ git merge bio-page
```

## view Remote Repositories (Mary)

```
$ git remote

origin
```

- `git remote` list the remote connections
- when you clone a repository, Git auto adds an `origin` remote pointing to the original repository
  under the assumption that you'll want to interact with it down the road.

```
$ git remove -v

origin  /Users/rhyme/Documents/Dev/Projects/Rhyme/my-git-repo (fetch)
origin  /Users/rhyme/Documents/Dev/Projects/Rhyme/my-git-repo (push)
```

- `git remote -v` list remote verbose

## Back to Our Repository, and Add Mary as a Remote

```
$ git remote add mary ../marys-repo
```

- so Mary has a `origin` remote pointing to us
- we has a `mary` remote pointing to mary

## Fetch Mary's Branches

we can use `remote branches` to access snapshots from another repository

```
$ git fetch mary
$ git branch -r

mary/bio-page
mary/green-page
mary/master
```

- `git branch -r` list our remote branches
- `git fetch` fetch branches from Mary's repository
  this will go to the `fetch` location shown in `git remote -v` and download all of the branches it finds there into our repository

- `remote branches` are always in the form `<remote-name>/<branch-name>`, so they will never be mistaken for local branches

- the `git fetch mary` only download Mary's repository at that time, they will not auto update with Mary
- our remote branches are not `direct links into` Mary's repository, they are read-only copies of her branches

## Check out a remote branch

- `git checkout mary/master`

this puts us in a `detached HEAD` state
our remotes branches are `copies` of Mary's branches
checking out a remote branch takes out HEAD off the tip of a `local branch`

- we can't continue developing if we're not on a local branch

to build on `mary/master` we either need to merge it into our own `local master` or create another branch
