# Quick OpenWrt SDK start

More detailed tutorial is [here](https://openwrt.org/docs/guide-developer/helloworld/chapter1)

## Download sdk
```bash
git clone https://git.openwrt.org/openwrt/openwrt.git source
git checkout v21.02.3 # checkout to last release
```

## Update and install feeds
```bash
./scripts/feeds update -a
./scripts/feeds install -a
```

## Run graphical configuration menu
```bash
make menuconfig
```

## Run make to build your firmware
```bash
make
```

## Adjust the Path variable

Suppose that your sdk folder is located here `/home/user/openwrt-sdk/openwrt-sdk-21.02.3`

Just add following path to PATH:
```bash
export PATH=/home/comarch_user/openwrt-sdk/openwrt-sdk-21.02.3/staging_dir/host/bin:$PATH
```
