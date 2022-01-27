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

