# Including feeds

[OpenWrt Feeds](https://openwrt.org/docs/guide-developer/feeds)

## Including package feed into the OpenWrt build system

It is a good manner to store folder with feeds separately, outside of sdk folder.

Imagine that libsnap7 folder from [Example lib package makefile](./makefile_feeds.md#example-lib-package-makefile) is located in `/home/user/mypackages`

1. We can link following packages feeds to sdk:
```bash
cd {sdk_directory}
nano feeds.conf
src-link mypackages /home/user/mypackages
```

2. Update and install following feeds:
```bash
cd {sdk_directory}
./scripts/feeds update mypackages
./scripts/feeds install -a -p mypackages
```

3. Check if libsnap7 is visible in menuconfig:
```bash
make menuconfig
```
