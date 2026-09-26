# notify-send

`notify-send` shows a desktop notification popup, handy for flagging when a long-running command finishes.

## Install notify-send
```bash
sudo apt-get install libnotify-bin
```

## Example
```bash
make && notify-send "Build finished"
```