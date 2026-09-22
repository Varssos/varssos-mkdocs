# Open Auto

## OpenDash

Instead of installing OpenAuto manually you should install [OpenDash](https://github.com/openDsh/dash) and install according to the readme.

## OpenAuto

!!! warning
    I had a lot of issues. Just don't use OpenAuto. OpenDash doesn't have many problems and it is up to date.

1. Prepare the recommended Raspberry Pi OS (Bullseye) image.
2. Update apt and fix problems with it, see [Apt Raspbian Repositories](./apt_repo_manager.md).
3. Follow the installation from the readme here: <https://github.com/humeman/openauto-patched-installer>

Problems:

- USB permissions: <https://github.com/f1xpl/openauto/wiki/udev-rules-(USB-permissions)>

```bash
sudo apt-get install mtp-tools
sudo apt-get install libmtp-runtime
```

Other sources:

- <https://github.com/openDsh/aasdk>
- <https://github.com/openDsh/openauto>

Missing package:

```bash
sudo apt-get install qtdeclarative5-dev
```

Last error in `make -j1` in openauto:

```
[ 83%] Linking CXX shared library /home/pi/openauto/lib/libopenauto.so
/usr/bin/ld: cannot find -lh264bitstream
```
