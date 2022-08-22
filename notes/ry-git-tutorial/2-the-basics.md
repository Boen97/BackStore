# The Basics

the fundamental Git workflow:
creating a repository, staging and committing snapshots, configuring options, and viewing the state of a repository

## initialize the Git repository

- `git init` to turn the directory into a Git repository
- `.git` directory stores all the tracking data for our repository

- an `untracked file` is one that is not under version control

## Stage a Snapshot

- `git add test1.txt` tells Git to start tracking `test1.txt`

we just add `test1.txt` to the `snapshot` for the next commit

- a `snapshot` represents the state of your project at a given point in time.

- Git's term for creating a snapshot is called `staging`
  because we can add or remove multiple files before actually commiting it to the project history

staging gives us the opportunity to group related changes into distinct snapshots
a practice that makes it possible to track the `meaningful` progression of a software project

## Commit the Snapshot

- `staging` telling Git what files to include in the next commit
- `committing` recording the staged snapshot with a descriptive message.

- staging file with the `git add` commit doesn't actually affect the repository in any significant way
  it just lets us get our files in order for the next commit

- only after `git commit` will our snapshot be recorded in the repository
- commited snapshots can be seen as a `safe` versions of the project.

Git never changes committed snapshots, which means you can do almost anything you want to your project without losing those `safe` revisions.

## view the Repository History

`git status` shows nothing, means that our current state matches what is stored in the repository
`git status` only show us `uncommitted changes`
to view our repository history, we need `git log` command

`SHA-1` checksum is the unique ID for the commit, which ensures that the commit will never be corrupted without Git knowing about it.

we can only see `staged changes`  with `git status`
`git log` only for commited changes

- `git log --oneline`
- `git log --oneline test1.txt`

## Configue Git

```
git config --global user.name "JakeRess"
git config --global user.email 296430507@qq.com
```

`--global` tells Git to use this configuration as a default for all of your repositories

## working directory, staged snapshot, committed snapshots

working directory <staged> will into staged snapshot
stage snapshot -> committed into committed snapshots
