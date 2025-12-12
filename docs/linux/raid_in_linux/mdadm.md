# mdadm

## Tools which can check status of your disk

### Print info about all block devices like disks, paritition, RAID, LVM etc
```
lsblk
```

### Print info about used and available disk space
```
df -Th
```

### Print info about filesystem, UUID for block device like RAIDs
```
sudo blkid /dev/md0
```

### Print status about mdadm RAIDs
```
cat /proc/mdstat
```

### Print file system table config
```
cat /etc/fstab
```

### Print gpt/disk array meta data
```
sudo mdadm --examine /dev/sdb
```


## How to create raid1(mirror) on clean 2 disks e.g. /dev/sdb and /dev/sdc (Ubuntu/Debian)

1. Install mdadm
```
sudo apt-get install mdadm
```

2. Check if disk drives are visible under /dev/sdb /dev/sdc etc
```
lsusb
sudo fdisk -l
```

3. If you have existing partitions on your disk drives and you want to erase them
```
sudo fdisk /dev/sdb
d
w
```

4. Create raid1
```
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc
```

5. Create ext4 fs on your raid
```
sudo mkfs.ext4 /dev/md0
```

6. Check raid status
```
cat /proc/mdstat
```

## How to assemble raid when filesystem and raid exist on both drives /dev/sdb and /dev/sdc

1. Examine disk content
```
lsusb
sudo mdadm --examine /dev/sdb
sudo mdadm --examine /dev/sdc
``` 

You should expect same magic, version, array UUID etc

2. Assemble raid under /dev/md0
```
sudo mdadm --assemble --run /dev/md0 /dev/sdc /dev/sdb
# or:
sudo mdadm --assemble --force /dev/md0 /dev/sdc /dev/sdb
```

3. Check raid status
```
cat /proc/mdstat
```

## How to assemble and mount automatically after reboot

1. Assuming that raid1 is created on /dev/md0 on device /dev/sdb and /dev/sdc
```
lsusb
sudo mdadm --examine /dev/sdb
sudo mdadm --examine /dev/sdc
cat /proc/mdstat
```

2. Setup mdadm.conf
```
sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf
# It should append sth like:
ARRAY /dev/md0 metadata=1.2 spares=1 UUID=7362a476:03f1fd56:c245f7ef:17807ed5
```

3. Update initramfs
```
sudo update-initramfs -u
```

4. Create mounting point
```
sudo mkdir -p /mnt/md0
```

5. Check uuid of RAID
```
sudo blkid /dev/md0
# Expected output
/dev/md0: UUID="e469300e-312d-44d3-b617-267dbc2f40c2" BLOCK_SIZE="4096" TYPE="ext4"
```

6. Update fstab
```
sudo nano /etc/fstab
# with:
UUID=e469300e-312d-44d3-b617-267dbc2f40c2  /mnt/md0  ext4  defaults  0  2
```

7. Reload daemons
```
systemctl daemon-reload
```

8. Test mounting
```
sudo mount -a
```



## How to umount mdadm raid
```
sudo umount /dev/md0
```

### If target is busy, check:
```
sudo lsof +f -- /mnt/md0

sudo mdadm --stop /dev/md0

systemctl stop smbd

# dockers
sudo systemctl stop docker.socket
sudo systemctl disable docker.socket

sudo systemctl stop docker
sudo systemctl disable docker
```

### Last resort with force?
```
sudo fuser -km /mnt/md0
```

### teardown stopped processes
```
systemctl start smbd

sudo systemctl enable docker.socket
sudo systemctl start docker.socket

sudo systemctl enable docker
sudo systemctl start docker
```



## How to remove mdadm raid
```
cat /proc/mdstat
sudo mount | grep /dev/md0
sudo umount /dev/md0
sudo fuser -mv /dev/md0
sudo mdadm --stop /dev/md0
sudo mdadm --remove /dev/md0
```
It was safe for me to remove raid and recreate it again(without data loss)

```
sudo mdadm --stop /dev/md0
sudo mdadm --remove /dev/md0
sudo mdadm --zero-superblock /dev/sdb
sudo mdadm --zero-superblock /dev/sdc
```


## How to setup mdadm with RAID1 in ansible


It is based on that role: `ansible-mdadm Github <https://github.com/mrlesmithjr/ansible-mdadm/tree/master>`_

1. Install galaxy dependency

ansible-galaxy install mrlesmithjr.mdadm

2. In ``run.yml`` add role like this

```
---
- hosts: nas
    become: yes
    vars:
    mdadm_arrays:
    # Define array name
    - name: 'md0'
    # Define disk devices to assign to array
    devices:
        - '/dev/sdc'
        - '/dev/sdd'
    # Define filesystem to partition array with
    filesystem: 'ext4'
    # Define the array raid level
    # 0|1|4|5|6|10
    level: '1'
    # Define mountpoint for array device
    mountpoint: '/mnt/md0'
    # Define if array should be present or absent
    state: 'present'
    # Set mount options (optional)
    opts: 'noatime'

    roles:
    - role: mrlesmithjr.mdadm
```

You can move that vars to your ``vars.yml``
