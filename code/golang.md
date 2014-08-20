# Golang

## Vim Golang syntax installation
```sh
# Copy Golang syntax file into Vim folder
Place $GOROOT/misc/vim/syntax/go.vim in ~/.vim/syntax/
# Put the following in ~/.vim/ftdetect/go.vim:
au BufRead,BufNewFile *.go set filetype=go
```
