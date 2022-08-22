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
