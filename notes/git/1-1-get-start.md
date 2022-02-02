## DVCS distributed verson control system

every client keep a copy of all data, and you don't need to worry about data lose

## the design of git
- stream of snapshots
- nearly every operations is local

## checksum-SHA-1 hash value

## generally git only add data

## three states
- modified
- staged
stage area is what will be commit next time
- committed

## check git version
git --version

## git config

- git config --system [path]/etc/gitconfig
- git config --global ~/.gitconfig
- default git config --local .git/config config specific to repostory

## view all your settings and where they come from 
git config --list
git config --list --show-origin

## your identity

git config --global user.name "Rhyme"
git config --global user.email jbw.ress@gmail.com

## your editor

git config --global core.editor emacs

## default branch name
when you run git init the default name of the branch
git config --global init.defaultBranch main

## git config --list

当同一个key有多个相同的值时，采用最后一个value

## git config user.name
检查某一个配置的属性值

> 凡是配置相关的，就找 git config 命令

## git config --show-origin user.name

## get help

- git help config 关于config命令的详细说明
- git config -h 关于config命令的简短说明

## init a repository in a existing directory
git init
git add
git commit

## git clone https://github.com/libgit2/libgit2 mylibgit
重命名但是并不会包含原来的文件夹的名字
