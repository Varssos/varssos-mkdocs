# fzf

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

## Shortcuts
CTRL-T  - get a list of files and directories
ALT-C   - get a list of directories
CTRL-R  - bash history



## Search syntax

- `.log !logcat` - all `.log` but not `logcat`


## Configs

```

```
