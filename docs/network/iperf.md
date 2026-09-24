# iperf

## Measuring network throughput between a host PC and a QNX device

On the QNX side (server):

```bash
iperf2 -s
```

On the host PC (client):

```bash
sudo apt install iperf
iperf -c 192.168.1.1
# Test both directions
iperf -c 192.168.1.1 -d
```

> Both sides must use the same major iperf version (iperf2 vs. iperf3) - their wire protocol and command-line flags are not compatible with each other.
