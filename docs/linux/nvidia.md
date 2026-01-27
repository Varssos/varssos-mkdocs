# Nvidia

## How to install nvidia drivers on debian based distros

Right now `nvidia-driver-580` is the most stable from drivers below:
```
nouveau
nvidia-driver-580
nvidia-driver-580-open
```


```
sudo apt update
sudo apt install nvidia-driver-580
sudo reboot
```


## How to diagnose issues with nvidia drivers

```
uname -r
nvidia-smi
lsmod | grep nvidia
xrandr
prime-select query
```


## Known issues with nvidia
### Black screen with multimonitors on system startup.
! This can run nvidia as main card and make eDP not available (amdgpu) which disable laptop monitor and enable all external monitors
Root cause:
lightdm start faster that Nvidia set all
Fix:
1. Edit grub
```
sudo nano /etc/default/grub
```
2. Add option: nvidia-drm.modeset=1
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nvidia-drm.modeset=1"
```

3. Update grub and reboot
```
sudo update-grub
sudo reboot
```

### Black screen on laptop monitor but external working on

It's when in `xrandr` output eDP is not visible

Fix:
1. Erase `nvidia-drm.modeset=1` from `/etc/default/grub`
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

2. Move xorg.conf to backup
```
sudo mv /etc/X11/xorg.conf /etc/X11/xorg.conf.backup
```

3. Change prime to on-demand
```
sudo prime-select on-demand
```


### High temperature even during brosing internet

What can reduce:
1. Disable graphics acceleration
```
chrome://settings/system
-> Disable: Use graphics acceleration when available
```

2. Change prime mode
```
sudo prime-select on-demand
sudo reboot
```

3. Set soft limit or power limit
```
nvidia-smi -q -d POWER
sudo nvidia-smi -pl 60
```


4. Monitor or control fan if possible

[CoolerControl OSS project](https://gitlab.com/coolercontrol/coolercontrol)


