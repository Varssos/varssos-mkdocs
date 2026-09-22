# Home Automation

[Home Assistant installation](https://www.home-assistant.io/installation/)

[How to start with Home Assistant on RPI](https://www.home-assistant.io/installation/raspberrypi)

## Setup HA on RPI4 with Docker

!!! important
    I assume that you want to set up HA on RPI4 with Raspberry Pi OS on Bullseye.

### Prepare Docker

```bash
sudo apt update
sudo apt upgrade
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/raspbian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=armhf signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/raspbian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo systemctl status docker
```

```bash
sudo usermod -aG docker $USER
newgrp docker
```

If the file doesn't exist, create `/etc/docker/daemon.json` and put in:

```json
{
    "group": "docker"
}
```

### Run the Home Assistant Docker Container

```bash
docker run -d   --name homeassistant   --privileged   --restart=unless-stopped   -e TZ=Europe/Warsaw   -v /home/seba/Documents/HomeAssistant:/config   --network=host   ghcr.io/home-assistant/home-assistant:stable
```

### Setup Home Assistant on the Webpage

Go to your browser and go to `RPI_IP:8123`.
