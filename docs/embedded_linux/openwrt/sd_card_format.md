# SD card format

If there is lack of some information, check this nice [tutorial](https://openwrt.org/docs/guide-user/storage/usb-drives)

[To manage partitions you can use fdisk](https://www.golinuxcloud.com/steps-to-format-sd-card-in-linux/)

Steps:

1. Before start, refresh the list of available software packages
```bash
opkg update
```

2. Install all packages

To handle filesystem:
```bash
opkg install block-mount kmod-fs-ext4 e2fsprogs
# Optionally:
opkg install cfdisk
# Handling usb:
opkg install kmod-usb-core kmod-usb2 kmod-usb-storage
```

3. List your connected devices
```bash
opkg install usbutils
lsusb -t
```

4. Check current file system
```bash
df -Th
```

5. If card exists as /dev/sda*/ e.g. /dev/sda1/ try to unmount:
```bash
umount /dev/sda1
```

Otherwise check which one is it
```bash
ls -l /dev/sd*
```

6. Format with EXT4 file system
```bash
mkfs.ext4 /dev/sda1
```

7. Mount sd card
```bash
mkdir /mnt/sdcard
mount /dev/sda1 /mnt/sdcard
```

8. Set fstab for automount after reboot
```bash
uci add fstab mount
uci set fstab.@mount[-1]='mount'
uci set fstab.@mount[-1].device='/dev/sda1'
uci set fstab.@mount[-1].fstype='ext4'
uci set fstab.@mount[-1].options='rw,noatime'
uci set fstab.@mount[-1].target='/mnt/sdcard'
uci set fstab.@mount[-1].enabled_fsck='1'
uci set fstab.@mount[-1].enabled='1'

uci commit
```

9. Check filesystem if mounted properly
```bash
df -Th
```

10. Verify mounted blocks info
```bash
block info
```

## Mounting SD card with volume label
```bash
opkg update
opkg install block-mount kmod-fs-ext4 e2fsprogs
opkg install kmod-usb-core kmod-usb2 kmod-usb-storage
opkg install usbutils

umount /dev/sda1
mkfs.ext4 -L sd_card /dev/sda1

mkdir /mnt/sdcard
mount /dev/sda1 /mnt/sdcard

uci add fstab mount
uci set fstab.@mount[-1]='mount'
uci set fstab.@mount[-1].label='sd_card'
uci set fstab.@mount[-1].fstype='ext4'
uci set fstab.@mount[-1].options='rw,noatime'
uci set fstab.@mount[-1].target='/mnt/sdcard'
uci set fstab.@mount[-1].enabled_fsck='1'
uci set fstab.@mount[-1].enabled='1'

uci commit
```

## Mounting OpenWrt feed

[sd_card feed to automate mounting sd card](./sd_card.tar.gz)
