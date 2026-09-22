# MergerFS and SnapRAID

!!! warning
    MergerFS and SnapRAID are beneficial if you have drives with different capacity. In my case I had drives with the same capacity and only 2 disk drives, so you can't use it like below. On the last step `snapraid sync` it will fail like this:
    ```
    Self test...
    You must have at least 2 'content' files in different disks.
    ```

Based on [MergerFs + SnapRAID](https://www.youtube.com/watch?v=tX5MA-c6Qq4)

In my case I have 2 disks. I want to make it a RAID1 or RAID5.

## Generate partitions and format disks

List available disks:
```bash
lsblk
```

Create partitions. Do this for both disks:
```bash
sudo fdisk /dev/sdb
g
n
Y
w
```

Install the tool needed to format:
```bash
sudo apt-get update
sudo apt-get install -y xfsprogs
```

Format both disks:
```bash
sudo mkfs.xfs /dev/sdb1
```

Check if it is visible:
```bash
lsblk
blkid
```

Add to fstab `/etc/fstab`:
```
# Data drives
UUID="000e0f42-6914-4606-849b-ad812cb21977"	/mnt/data1	xfs	defaults	0	2

# Parity drive
UUID="e5f1d86c-8624-4bf8-a7b4-9d97f68ce767"	/mnt/parity1	xfs	defaults	0	2
```

Create directories to mount:
```bash
sudo mkdir -p /mnt/data1
sudo mkdir -p /mnt/parity1
```

## Setup mergerFS
```bash
sudo apt install -y fuse mergerfs
```

Add to fstab `/etc/fstab`:
```
# MergerFS
/mnt/data*	/mnt/pool	fuse.mergerfs	defaults,allow_other,use_ino,hard_remove	0	0
```

Create directory to mount:
```bash
sudo mkdir -p /mnt/pool
```

Mount all:
```bash
sudo mount -a
```

Pool should be visible in `df -h`:
```
/mnt/data1      932G  6,6G  925G   1% /mnt/pool
```

## SnapRAID
Install:
```bash
sudo apt install snapraid
```

Create the SnapRAID config:
```bash
sudo nano /etc/snapraid.conf
```

Fill it with this content:
```
parity /mnt/parity1/snapraid.parity
data d1 /mnt/data1/
content /mnt/data1/.snapraid.content
exclude /Backup/
exclude /tmp
exclude *.bak
autosave 100
```

Then run SnapRAID:
```bash
snapraid sync
```
