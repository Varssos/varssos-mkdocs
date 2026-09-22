# Linux networking

[Nice tutorial about general information about linux networking](https://developers.redhat.com/blog/2018/10/22/introduction-to-linux-interfaces-for-virtual-networking#vxlan)

## Check network interfaces
```bash
ifconfig
```

## ARP

Address Resolution Protocol. The primary function of this protocol is to resolve the IP address of a system to its MAC address, hence it works between layer 2 (Data link layer) and layer 3 (Network layer). You can check connected devices and DHCP clients.

```bash
arp
```

## Checking open ports

```bash
nmap {ip}
```

See [nmap](./nmap.md) for more advanced usage.

## Quick diagnostic commands

| Command | Description |
|---|---|
| `arp -n` | show the address cache table (resolved IP <-> MAC mappings) |
| `nc {ip} {port}` | check connectivity to a port |
| `ping -I {interface} {ip}` | ping through a chosen interface |
| `netstat -a -n \| grep ESTABLISHED` | check active established sessions |
| `nmap {ip}` | scan open ports for an ip |
