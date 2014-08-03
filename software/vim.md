# Vim

## .vimrc
```sh
" Always at 8!
set tabstop=8
" converts tabs to white space
set expandtab
set shiftwidth=2
set softtabstop=2

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
