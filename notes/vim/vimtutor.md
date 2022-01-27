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

## d number motion
d2w 删除两个单词

## operating on lines
dd 删除行
2dd 删除2行

