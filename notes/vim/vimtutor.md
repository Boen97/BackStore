## move
h left
j down
k up
l right

## exiting vim
ESC
:q! discard any changes

## delete
x delete a word under cursor

## insert
i insert before the cursor

## append
A move cursor to the line end and append

## editing file
:wq save a file and exit

## deletion commands
d delete operator 操作符
  motions: 动作
  - w
  - $
  - e
dw until the start of the next word.
d$ delete to the end of the line
de to the end of the current word, INCLUDING the last character.

## count motion
w move word forward
e move to the end of word
0 move to the start of line
2w
3e
b back a word

## d number motion
d2w 删除两个单词

## operating on lines
dd 删除行
2dd 删除2行

## the undo command
x delete a word
u undo
U return the line to its original state
C-R undo the undo's

## the put command
p put the pre deleted line after the cursor

## the replace command
r replace the character at the cursor

## the change command
ce to change until the end of the word
cc chang the whole line
cw change the word
c$ change to the end of line

## cursor location and file status
C-g show your location in the file and file status
G to the bottom of the file
gg to the head of the file
485 G return to the 485 line

## the search command
/errroor
n next find
N next find in the opposite direction
?errror search backwards
Ctrl-o go back to you came from before search

## matching parentheses search
% to to match parenttheses

## page up down
Ctrl + d
Ctrl + u

## put the line of screen
z-enter put the line to top of screen
zz put the line to the center of screen
zb put the line to the bottom of screen

## the substitute command
:s/thee/the change the first occurence of 'thee' in the line
:s/thee/the/g sucstitude globally in the line
:485,487s/thee/the/g 替换指定行内
:%s/thee/the/g 替换整个文件
:%s/thee/the/gc substitude the whole file with a prompt

## execute an external command
:!ls


## save file
:w filename save current buffer to the target file

## select text to write
v press v
then move the cursor to select text
:w TEST save the select text to TEST

## retrieving and merge files
:r filename 将文件中的内容添加到光标所在位置
:r !ls 将命令执行结果添加到光标所在处

## open command
o open a line below the cursor
O open a line above the cursor

## the append command
a insert text after the cursor
i insert text before the cursor
A append text after the end of line

## another to replace
R 可以连续替换一个字符


## copy and paste text
y copy select vition
yy copy the line
$ move to the end of line
yw copy the word
p put that copy text







