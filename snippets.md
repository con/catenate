## Vim shortcut: one sentence per line

Break up the current line, one sentence per line.

`nnoremap <Leader>s :execute 's/\%>' . col('.') . 'c\(\.\)\s\+/\1\r/'<CR>`

## function: `exclip`: execute a file, copy file contents and outputs

```sh
function exclip() {
    local file="$1"

    if [[ ! -f "$file" ]]; then
        echo "Error: File not found: $file"
        return 1
    fi

    if [[ ! -x "$file" ]]; then
        echo "Error: File is not executable: $file"
        return 1
    fi

    local contents=$(cat "$file")
    local output=$("$file" 2>&1)

    local result="# $file
\`\`\`
$contents
\`\`\`
\`\`\`
$output
\`\`\`"

    echo "$result" | xclip -selection clipboard
    echo "$result"
}
```
