# Jellyfin

[Install jellyfin on Ubuntu](https://jellyfin.org/docs/general/installation/linux/)

```bash
sudo apt install apt-transport-https
curl https://repo.jellyfin.org/install-debuntu.sh | sudo bash
```

## Problems with Jellyfin

### The path could not be found

Jellyfin just doesn't have access to your media directory. Try:

```bash
sudo setfacl -m u:jellyfin:rx /home/seba_nas
```
