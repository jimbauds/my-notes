# Vim

## .vimrc
```sh
" Always at 8!
set tabstop=8
" converts tabs to white space
set expandtab
set shiftwidth=2
set softtabstop=2

" Only if my terminal windows are dark themed.
set background=dark
" Show information about the current command
set showcmd
" Show INSERT type
set showmode

filetype off
filetype plugin indent off
"set runtimepath+=$GOROOT/misc/vim
set rtp+=$GOROOT/misc/vim
filetype plugin indent on
syntax on
" set list listchars=tab:\ \ ,trail:·
" set nowrap 
" set wildmode=list:longest
execute pathogen#infect()
```
## Commands
```sh
w #=> jump to the next word
e #=> jump tp the end of the word
b #=> jump back
0 #=> jump to the beginning of the line
$ #=> jump to the end of the line
ctrl+u #=> jump half of the document up
ctrl+d #=> jump half of the document down
r #=> replace text
i #=> insert at the cursor location
a #=> append at the cursor location
A #=> append at the end of the line
o #=> Insert a newline
d [modifier] #=> to delete as follows
  w - entire word
  e - to end of word
  b - back one word
  $ - to end of line
  dd delete the entire line regardless of the cursor position
u #=> undo
U #=> Restore entire line to original state
y #=> yank (copy)
p #=> paste after the cursor
P #=> paste before the cursor
H #=> Go to the top of the screen
M #=> Go to the middle of the screen
L #=> Go to the end of the screen
gg #= Go to the beginning of the file
G #=> Go to the end of the document


:sh #=> Return to shell without closing the open document
exit #=> Exirt from the shell and return to Vim

:ls #=> List buffer
:b4 #=> switch to buffer 4
:b# #=> switch to next buffer
:bf #=> switch to first buffer
:bl #=> switch to last buffer
:bd #=> Destroy current buffer

/soleil #=> search the word "soleil"
:n #=> go to the next occurence

< or > #=> Indent a selected block of code

:e <filename> #=> Open new file
:e #=> Reload the current file

:s/SearchFor/ReplaceWith/g #=> Search and Replace text
?Find/Replace/g #=> Search and Replace (Reverse)
:s/Find with Confirmation/Each one/gc #=> Find and Replace with confirmation

% #=> Jump to the next bracket

:split filename #=> Open new file in split mode
ctrl+wq #=> Quit current window


```














