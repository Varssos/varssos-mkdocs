# Brother printer on Linux

1. Follow the printer driver installer instructions:
```bash
gunzip linux-brprinter-installer-*.*.*-*.gz
sudo bash linux-brprinter-installer-*.*.*-* Brother machine name
# Next in my case:
DCP-J315W
Will you specify the Device URI? [Y/n] ->Y
13     # 13 (I): Specify IP address.
192.168.X.X  # Type printer IP
# Many y y y 
```

2. Now you are able to print

3. Setup scanner
```bash
sudo apt-get install sane xsane
```

4. Restart PC
5. Now you should see the XSane app in the system and be able to scan documents
