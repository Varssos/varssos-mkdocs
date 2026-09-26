# Admin tools


## Change port for ssh

Edit the SSH daemon config and add the new port under `Port`:
```bash
sudo nano /etc/ssh/sshd_config
```

On SELinux-enforcing systems, list the ports already allowed for the `ssh_port_t` type, then allow the new one:
```bash
sudo semanage port -l
sudo semanage port -a -t ssh_port_t -p tcp 2022
```

## Show commands run by another user

Check what commands any other user currently working on the system has run:
```bash
ps aux | grep -v $USER | tail -1
```

## Run a priority-lowered background search

Search the whole system in the background for file names matching a pattern (`*user*`), redirect errors to null, results to a file, and lower the priority of the command to the lowest:
```bash
nice -n20 find / -name "*user*"  2>/dev/null >/tmp/results &
```

## Manage users on linux

[How to change username usergroup, askubuntu thread](https://askubuntu.com/questions/34074/how-do-i-change-my-username) 

[How to change hostname on linux](https://www.hostinger.com/tutorials/linux-change-hostname)


## DNF (RPM-based distros)

[Install PHP 8 on CentOS](https://www.tecmint.com/install-php-8-on-centos/)

## Extra permissions

[SUID, SGID and sticky bit explained](https://www.thegeekdiary.com/linux-interview-questions-special-permissions-suid-sgid-and-sticky-bit/)

```bash
setfacl -m u:Kermit:rw echo.txt
getfacl echo.txt

umask 0006
```

## SMTP mail server

After setting up the smtp server according to the [poczta.pdf](./poczta.pdf) instructions, you need to unblock the ports:

```bash
firewall-cmd --add-service=smtp --permanent
firewall-cmd --add-service=pop3 --permanent
firewall-cmd --add-service=pop3s --permanent
firewall-cmd --add-service=imap --permanent
firewall-cmd --add-service=imaps --permanent
```

On the client, on another device, install e.g. thunderbird:

```
user: student
address: student@alma1.test.lab
pass:...
```

