# NoMachine

## Install NoMachine

```bash
cd ~/Downloads
curl https://download.nomachine.com/download/8.7/Linux/nomachine_8.7.1_1_amd64.deb --output nomachine_8.7.1_1_amd64.deb
sudo dpkg -i nomachine_8.7.1_1_amd64.deb
```

Or more generic:
```bash
cd ~/Downloads
wget https://www.nomachine.com/free/linux/64/deb -O nomachine.deb
sudo apt install ./nomachine.deb
```

## Check NoMachine process

```bash
systemctl status nxserver
```

## Uninstall NoMachine

```bash
systemctl stop nxserver
systemctl disable nxserver
sudo dpkg -r nomachine
sudo dpkg --purge nomachine
```

## NoMachine FAQ

[NoMachine Knowledge Base](https://kb.nomachine.com/AR03P00973)

### Black screen nomachine

```bash
sudo systemctl stop gdm
sudo /etc/NX/nxserver --restart
```

When back to the office try to ssh and:
```bash
sudo systemctl start gdm
# if it didn't bring the physical screen to life do
sudo reboot
```
