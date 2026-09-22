# Installing OpenWrt image

## Image download

Get firmware from [firmware selector](https://firmware-selector.openwrt.org/)

Or [OpenWrt downloads](https://openwrt.org/downloads)

Or build your own with SDK

## Send via scp on device

{user}: sshroot/root:
```bash
scp {image_file} {user}@{ip}:/tmp
```

## OpenWrt system upgrade
```bash
sysupgrade -v -c {image_file}
# -c attempt to preserve all changed files in /etc/
# -v more verbose
```
