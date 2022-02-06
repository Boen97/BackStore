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

