## Vim shortcut: one sentence per line

Break up the current line, one sentence per line.

`nnoremap <Leader>s :execute 's/\%>' . col('.') . 'c\(\.\)\s\+/\1\r/'<CR>`

