# Ubuntu post installation

What to do after: https://github.com/Varssos/ansible_setup_my_host

Add to ansible:

check id -nG

If dialout is missing, run sudo usermod -aG dialout "$USER"

Reboot is needed to see any changes


## TODO:

- [x] Add weeknumber to calendar
`Date & Time` -> Week Day `V`
- Install nvidia drivers


## Manual verify:

- [x] bashrc:
```
bashreload
```

- [x] copyq

Open `copyq`
`ctrl+shift+v`

- [x] dotfiles
```
ls -la ~/dotfiles
```

- [x] fzf
`ctrl+t`

- [x] kitty
```
ls -la ~/.config/kitty/
```

- [x] tmux

Turn on tmux and check if my custom theme is visible

- [x] vs code extension
```
code --list-extensions
```







