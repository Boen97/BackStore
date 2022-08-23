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
