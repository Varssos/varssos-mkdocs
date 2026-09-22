# RDP on RPI Bullseye

!!! warning
    **Black screen after setting up RDP?** You cannot log in twice with the same account using xrdp on Raspberry Pi OS Bullseye (Debian 11). You have to disable autologin or create another user, and remove the user from the `video` and `render` groups.

## How to Set Up RDP on RPI?

A general description of how to set up RDP on Linux is available in the Linux section.

Install xrdp:

```bash
sudo apt update
sudo apt install xrdp
```

Enable xrdp after reboot:

```bash
sudo systemctl enable --now xrdp
```

Install ufw:

```bash
sudo apt install ufw
```

Open a firewall port:

```bash
sudo ufw allow from any to any port 3389 proto tcp
```

Remove the user from the video and render groups:

```bash
sudo gpasswd -d $USER video
sudo gpasswd -d $USER render
```

Disable autologin:

```bash
sudo raspi-config
```

Then select `System options` -> `Boot / Auto Login` -> `Desktop GUI, requiring user to login`.
