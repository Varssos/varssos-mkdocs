# GRUB

GNU GRUB (grand unified bootloader)

## Choose linux kernel version

1. Edit GRUB setup file:
```bash
sudo nano /etc/default/grub
```
2. Set:
```
GRUB_SAVEDDEFAULT=true
GRUB_DEFAULT=saved  ## or: GRUB_DEFAULT="1>2" # where 2 is index on grub menu (starting from 0)
GRUB_TIMEOUT_STYLE=menu
GRUB_TIMEOUT=10
```
3. Update GRUB information to apply changes:
```bash
sudo update-grub
```
4. Reboot
5. Choose `Advanced options for Ubuntu` -> latest kernel version/desired version
6. Check current kernel version:
```bash
uname -r
```

## Change kernel version with grub customizer

[How to boot into an older kernel](https://itsfoss.com/boot-older-kernel-default/)

```bash
sudo add-apt-repository ppa:danielrichter2007/grub-customizer
sudo apt update
sudo apt install grub-customizer
```

1. Select the desired kernel entry and use the arrow (displayed on the top menu) to move it up the order.
2. `General settings` -> `default entry:` `predefined:` <here_choose your kernel version>
