## Vim shortcut: one sentence per line

Break up the current line, one sentence per line.

`nnoremap <Leader>s :execute 's/\%>' . col('.') . 'c\(\.\)\s\+/\1\r/'<CR>`

## function: `exclip`: execute a file, copy file contents and outputs

Execute a script and copy both the script contents and output to clipboard in markdown format.
By default wraps content in collapsible `<details>` tags for GitHub.
Use `--plain` for simple markdown format.

```sh
function exclip() {
    local file=""
    local plain=false

    # Parse arguments
    while [[ $# -gt 0 ]]; do
        case $1 in
            --plain) plain=true; shift ;;
            *) file="$1"; shift ;;
        esac
    done

    if [[ -z "$file" ]]; then
        echo "Error: No file specified"
        return 1
    fi

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

    local result
    if $plain; then
        result="# $file
\`\`\`
$contents
\`\`\`
\`\`\`
$output
\`\`\`"
    else
        result="<details><summary>$file</summary>

\`\`\`
$contents
\`\`\`
</details>

<details><summary>Output</summary>

\`\`\`
$output
\`\`\`
</details>"
    fi

    echo "$result" | xclip -selection clipboard
    echo "$result"
}
```
