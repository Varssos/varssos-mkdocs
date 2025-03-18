# ESP usb chip drivers


## How to install usb drivers on linux
```
lsusb
```
Silicon Labs CP210x → CP2102 lub CP2104
QinHeng Electronics CH340 → CH340G / CH340C


- CH340G/CH340C

```
sudo apt update
sudo apt install linux-modules-extra-$(uname -r)
sudo modprobe ch341
```

- CP2102

```
sudo apt update
sudo apt install cp210x-dkms
sudo modprobe cp210x
```


```
sudo usermod -a -G dialout $USER

```