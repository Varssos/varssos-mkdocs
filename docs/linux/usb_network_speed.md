# Usb network speed

## Check usb version on usb hub network adapter 

```
cat /sys/class/net/enxa0cec892f7e9/device/../speed
```

10000 → USB 3.1 Gen2
5000 → USB 3.0
480 → USB 2.0

## Check actaul bandwidth between host and device

sudo apt install iperf

One side
```
iperf2 -s
```

Other side:
```
iperf -c 192.168.1.1
```