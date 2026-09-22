# SSH server

Nice tutorial how to configure ssh server on ubuntu is [here](https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/)

## Install openssh-server

```bash
# Upgrade if needed
sudo apt-get update
sudo apt-get upgrade

# Then install openssh-server
sudo apt-get install openssh-server
```

## Enable ssh service

```bash
sudo systemctl enable ssh
```

## Start ssh service

```bash
sudo systemctl start ssh
```

## Verify ssh service

```bash
sudo systemctl status ssh
```

## Unblock ports if needed

```bash
sudo ufw allow ssh
sudo ufw enable
sudo ufw status
```
