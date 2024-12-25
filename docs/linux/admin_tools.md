# Admin tools


## Change port for ssh
```
sudo nano /etc/ssh/sshd_config
listing port: sudo semanage port -l
sudo semanage port -a -t ssh_port_t -p tcp 2022
```

## Manage users on linux

[How to change username usergroup, askubuntu thread](https://askubuntu.com/questions/34074/how-do-i-change-my-username) 

[How to change hostname on linux](https://www.hostinger.com/tutorials/linux-change-hostname)


## SWAP


Increase swap

```
sudo dd if=/dev/zero of=/var/swap.fs bs=1M count=1024
ls -al /var/swap.fs
sudo chmod 600 /var/swap.fs
sudo swapon /var/swap.fs
sudo nano /etc/fstab
echo "/var/swap.fs none swap defaults 0 0" >> /etc/fstab
```


On file
```
sudo dd if=/dev/zero of=/var/nowa.fs bs=1M count=1024
sudo mkfs.ext4 /var/nowa.fs
sudo mkdir /mnt/partzpliku
sudo mount /var/nowa.fs /mnt/partzpliku/
tail -1 /etc/mtab
```

