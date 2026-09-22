# VPN problems

## When connected to l2tp vpn some services are not available

I changed internet supplier and I had problems with connecting to some domains.
**Solution:** Change ppp0 interface mtu from 1400 -> 1200

**Temporary**

```bash
sudo ifconfig ppp0 mtu 1200
```

**Permanent**

!!! warning
    Permanent solution doesnt work for me

```bash
sudo nano /etc/dhcp/dhclient.conf
```

Fill with:

```
interface "ppp0" {
default interface-mtu 1200;
supersede interface-mtu 1200;
}
```

Restart networking service:

```bash
sudo service networking restart
```

Bring up the interface:

```bash
sudo ifup ppp0
```

Check result:

```bash
sudo ifconfig | grep mtu
```
