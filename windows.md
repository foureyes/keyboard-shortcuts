# Windows 10 Keyboard Shortcuts

## Vim in WSL

### Visual select to Windows 10 clipboard

`ctrl + c`

https://stackoverflow.com/questions/44480829/how-to-copy-to-clipboard-in-vim-of-bash-on-windows

```
" copy (write) highlighted text to .vimbuffer
vmap <C-c> y:new ~/.vimbuffer<CR>VGp:x<CR> \| :!cat ~/.vimbuffer \| clip.exe <CR><CR>
" paste from buffer
map <C-v> :r ~/.vimbuffer<CR>
```
## Emoji

### Emoji Keyboard

`Windows + .`
