# fzf

`fzf` is a general-purpose fuzzy finder: pipe any list of lines into it (files, processes, git branches, history...) and it lets you interactively filter/select from them.

## Configs

```bash
## Install bat and use batcat on ubuntu?
export FZF_DEFAULT_OPTS="--style full"
export FZF_CTRL_T_OPTS="
  --walker-skip .git,node_modules,target
  --preview 'batcat -n --color=always {}'
  --bind 'focus:transform-header:file --brief {}'"

source /usr/share/doc/fzf/examples/completion.bash
```

## Shortcuts (key bindings, once `key-bindings.bash`/`.zsh` is sourced)

| Shortcut | Action |
|---|---|
| `CTRL-T` | Get a list of files and directories |
| `ALT-C` | `cd` into a fuzzy-selected directory |
| `CTRL-R` | Fuzzy-search bash history |

## Fuzzy completion (`**<TAB>`, once `completion.bash`/`.zsh` is sourced)

Trigger fuzzy completion for a command's argument by typing `**` then `<TAB>`. fzf infers what to list based on the command:

- `cat **<TAB>` - fuzzy completion for files and directories
- `cd **<TAB>` - fuzzy completion restricted to directories
- `kill -9 **<TAB>` - fuzzy completion from the running processes list (picks the PID)
- `ssh **<TAB>` - fuzzy completion from known hosts
- `export **<TAB>` / `unset **<TAB>` - fuzzy completion from environment variable names
- `<TAB>` or `<Shift-TAB>` for multiple select, deselect from list

## Search syntax

- `.log !logcat` - all `.log` but not `logcat`
