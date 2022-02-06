## git status
## git add
## short status
- git status -s 
- git status --short
  - 左边的代表stage area 的状态,右边代表 the status of the working tree 
  - ?? untracked
  - A  new file added and staged
  - MM file modified and staged and modified again
  - M  file modified and staged
## .gitignore
- blank lines or lines starting with # are ignored
- standard global patterns working
1. *
   match zero or more characters
2. [abc]
   match a b c
3. [0-9]
4. ?
   match one character
5. a/**/z 
   match nested directories
6. !lib.a
   do track lib.a, even though you're ignoring .a files above
7. /TODO
   ignore the TODO file in the current directory, not subdire/TODO
8. build/
   ignore all files in any directory named build
9. doc/*.txt
10. doc/**/*.pdf

> git ignore template https://github.com/github/gitignore

- the root gitignore applies recursively to the entire repository
- subdirectory .gitignore applies to its scope location
## commit your changes
- git commit -m ""
## skipping the stage area
- git commit -a ""
  stage all tracked files and commit
## removing files
- git rm README
- git rm --cached README
- git rm log/\*.log
- git rm \*~
## viewing the commit history
- git log
- git log -p show diffs
- git log -p -2 limit length
- git log --state
- git log --pretty=oneline
- git log --pretty=format:"%h - %an, %ar"
- git log --graph
## limiting log output
- git log -2
- git log --since=2.weeks
- git log --since="2008-10-01"
- git log --before="2008-10-11"
- git log --author="Jake Ress"
- git log --grep="Hellp"
- git log -S function-name
- git log -- dev/rhymechiang
- git log --no-merges
