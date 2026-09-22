# ZFS

[ZFS on Linux. Proxmox](https://pve.proxmox.com/wiki/ZFS_on_Linux)

In my case I have 2 disks `/dev/sdb` and `/dev/sdc`. I want to make it a RAID1.

Check disks:
```bash
lsblk
sudo fdisk -l
```

## Install ZFS
```bash
sudo apt install -y zfsutils-linux
```

## Create ZFS pool
```bash
sudo mkdir -p /mnt/nas_pool
sudo zpool create -m /mnt/nas_pool nas_pool mirror /dev/sdb /dev/sdc
```

## Check pool status
```bash
sudo zpool status
```
