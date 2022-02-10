SPC + f + e 打开 spacemacs 相关配置文件
SPC + f + e + R reload configuration file
SPC + f + f find files
SPC + h + l help documentation of layer
SPC + h + SPC configuration of specific packages within a layer
Dotfile(.spacemacs)
SPC + SPC + dotspacemacs/install create a dotfile in your home directory
SPC + m major mode leader key
SPC + ? search key bindings
narrow search key bindings SPC\ b
SPC + h + d describe functions
emacs -nw open emacs on terminal

## process
- SPC a p list process
- j k navigate
- d delete process
- q quit process and close the buffer
## treemacs
- M-0 toggle treemacs
- SPC 0 toggle treemacs
## undo
Ctrl-/ hybrid mode undo
## formate code
SPC m =
, = = 
## multi-term
SPC a t s m
- next multi-term SPC m n
- SPC m p
## 在window select时，使用 tab 可以实现预览的效果
## show errors at point
SPC e x
## uncomment
SPC c l
## paste kill ring
SPC r y
## working with big project with multi sub projects
go to the sub project path , and touch .projectile
M-x projectile-add-known-project
M-x projectile-remove-known-project
## treemacs create file dir
c f 
c d
d delete node
q hide treemacs
R rename
## M-x custmize group doom-mode-line / monokai
## treemacs copy file
yf
## toggle fold
za
zo
## tab 不管是在后面还是前面，都会自动对齐 tab
## html tag fold unflod
SPC m z
## dd 能够直接删除 flod 的内容
## ivy swiper search 
SPC s s 能够实现在该文件中搜索 symbol 的效果
## web mode element select
C-c C-e s
## next error
SPC e n
