## emacs states
emacs states(evil insert state) just like vim mode(insert mode, visual mode)

## minor mode
一个buffer 可以有多个 minor mode(小功能)

## major mode
major mode 决定如何编辑当前的buffer,例如python-mode
一个buffer只能有一个major mode

## Layers
layer similar to vim plugins，例如 python layer
一个 layer 包含了多个 package, 每个 package 完成对应的功能

## transient-states
不用重复输入leader key
q quit transient state

## running commands
SPC + SPC could run any emacs commands

## buffers
SPC + b

## windows
just like splits in vim
SPC w v vertical split
SPC w s horizontal split
SPC w h/j/k/l navigate among windows
SPC w H/J/K/L move current window
SPC w . window transient state

## Files
SPC f f search files in the current directory
SPC f r search recent open files
SPC f s save file
:x save and quit file
:e <file> open file

## the help system
SPC h d f
SPC h d k see a for key binding and show what it is bound
SPC h d v search variables


## exploring
SPC h SPC list all layers and view files from the layer
SPC ? list all key bindings

## regular expression syntax

## customization

### .spacemacs file
 - four top level functions in the file
  1. /layers
  2. /init
  3. /user-init
  4. /user-config

- SPC f e d open .spacemacs
- SPC f e D update .spacemacs

## clear high light search
SPC s c