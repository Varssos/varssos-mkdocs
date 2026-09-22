# Getting started with BuildRoot

This short tutorial is based on [this article](https://www.digikey.com/en/maker/projects/intro-to-embedded-linux-part-1-buildroot/a73a56de62444610a2187cd9e681c3f2)

## Install BuildRoot
```bash
sudo apt update
sudo apt upgrade
sudo apt install -y git build-essential libncurses5-dev
git clone git://git.buildroot.net/buildroot
cd buildroot
```

## Build Embedded Linux Image

1. Check configuration for your board (or create your own one):
```bash
ls configs
```
2. Set up the configuration for your board (e.g. stm32mp157a_dk1_defconfig):
```bash
make stm32mp157a_dk1_defconfig
```
3. Adjust kernel and default package options:
```bash
make menuconfig
```
4. Build the image:
```bash
make
```
5. Check output binary:
```bash
ls -la output/images
```

## Copy Image to SD Card

1. Insert SD card
2. List information about all available or the specified block devices:
```bash
lsblk
```
3. If necessary, unmount pre-existing partitions, e.g.:
```bash
sudo umount /media/sgmustadio/boot
sudo umount /media/sgmustadio/rootfs
```

4. Copy the .img file to the raw SD card (replace mmcblk2 with your sd card destination):
```bash
sudo dd if=/output/images/sdcard.img of=/dev/mmcblk2 bs=1M
```

## Boot

1. Connect serial to USB cable connected to destination device and type:
```bash
dmesg | tail
```
2. Find out where the USB converter is located, e.g. /dev/ttyUSB0
3. Install serial terminal program. E.g. picocom:
```bash
sudo apt install -y picocom
```

4. Add user to dialout group to avoid problem with permission denied instead of using sudo each time:
```bash
sudo usermod -a -G dialout $USER
```

5. Check user groups:
```bash
groups $USER
```
