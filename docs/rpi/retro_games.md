# Retro Games on RPI

[Polish tutorial about RPI game emulators](https://www.youtube.com/watch?v=FvrqVLN9JMI)

## Retro Emulator ROMs

Find how to use that torrent:
<https://punkwhore.com/arcadepunks/2021-3/tor/Arcade.Reboot.Extended.Rpi4-Wolfanoz.torrent>

Games (ROMs) with images already prepared are available here: `arcadepunks.com`

It is probably the best idea.

## Raspberry Pi Imager

```bash
sudo snap install rpi-imager
```

## Batocera

Batocera images already include Kodi, so you can switch from Batocera to Kodi and upload images/music etc. from your mobile phone and share YouTube videos.

1. Go to <https://batocera.org/download>
2. Choose your platform and download the image.
3. Put the image on an SD card via your PC.
4. Run rpi-imager.
5. Choose OS -> `Use custom` and select the downloaded image.
6. Choose storage - this SD card.
7. Write.
8. Eject the SD card and put it in the RPI.
9. Connect a gamepad, HDMI, power supply and just play :)

Batocera commands (e.g. if you want to exit a game): <https://wiki.batocera.org/basic_commands>
