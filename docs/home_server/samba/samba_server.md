# Samba server

This tutorial is based on [Install and Configure Samba on Ubuntu](https://ubuntu.com/tutorials/install-and-configure-samba#1-overview)

## Install Samba server
```bash
sudo apt update
sudo apt install samba
```

### Edit Samba config file
```bash
sudo nano /etc/samba/smb.conf
```

Fill with:
```ini
[md0]
  comment = Samba on Ubuntu
  path = /mnt/md0
  read only = no
  browsable = yes
  public = yes
  writable = yes
```

### Set up Samba password for your user account
```bash
sudo smbpasswd -a $USER
```

### Restart Samba service and check status
```bash
sudo service smbd restart
sudo service smbd status
```

## Remove Samba server
```bash
sudo apt-get autoremove samba samba-common -y
sudo apt-get purge samba samba-common -y
```
