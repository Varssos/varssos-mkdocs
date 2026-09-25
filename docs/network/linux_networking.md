# Linux networking

[Nice tutorial about general information about linux networking](https://developers.redhat.com/blog/2018/10/22/introduction-to-linux-interfaces-for-virtual-networking#vxlan)

## Check network interfaces
```bash
ifconfig
```

## ARP

Address Resolution Protocol - resolves the IP address of a system to its MAC address. It works between layer 2 (data link layer) and layer 3 (network layer). Use it to check connected devices and DHCP clients.

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

## DNS issues

If DNS resolution fails (e.g. VPN or captive network breaks DNS-over-TLS negotiation with `systemd-resolved`), try disabling DNS-over-TLS on the affected interface:

```bash
sudo resolvectl dnsovertls eno1 off
```

Check current DNS status with:

```bash
resolvectl status
```
