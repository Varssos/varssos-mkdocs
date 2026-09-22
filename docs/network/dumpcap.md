# Dumpcap

## How to list available interfaces
```bash
dumpcap -D
```

## Basic capture on an interface
```bash
dumpcap -i enp2s0f0 -w /tmp/capture.pcap
dumpcap -i 1 -w /tmp/capture.pcap # 1 is the number of the interface from dumpcap -D
```

## Dumpcap with a ring buffer
```bash
dumpcap -i enp2s0f0 -w /tmp/capture.pcap -b filesize:1000000 -b files:10   # size is in kB, in this case 1GB, 10 files
```
