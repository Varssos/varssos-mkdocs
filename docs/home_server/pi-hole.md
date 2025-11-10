# Pi-hole

[Pi-hole documentation](https://docs.pi-hole.net/)

## Pi-hole with docker

1. Create docker-compose.yml content
```
nano docker-compose.yml
```

2. Fill with [Pi-hole documentation - docker](https://docs.pi-hole.net/docker/)

3. Run docker with
```
docker compose up -d
```

### Remove pi-hole docker
```
docker stop pihole
docker rmi pihole/pihole --force
```


## Pi-hole + unbound

### Install pi-hole with docker
1. Install pi-hole with docker as above but with environment:
```
FTLCONF_dns_upstreams: '127.0.0.1#5335'
```

### Install unbound

1. Install unbound
```
sudo apt install unbound
```

2. Fill `/etc/unbound/unbound.conf.d/pi-hole.conf` with [Configure unbound](https://docs.pi-hole.net/guides/dns/unbound/?h=unbound#configure-unbound)
```
nano /etc/unbound/unbound.conf.d/pi-hole.conf
```

3. Restart service

```
sudo service unbound restart
dig pi-hole.net @127.0.0.1 -p 5335
```

### Remove unbound
```
sudo apt remove unbound -y
sudo rm -rf /etc/unbound/unbound.conf.d/pi-hole.conf
```


## Issue with pi-hole and blocking ads?
1. Chrome bypass dns?
Solution: Settings->Privacy and security -> Security -> Use secure DNS -> OFF

2. Ads not visible on https://www.independent.co.uk/ but visible on other regional websites? 
Solutino: extend block list

3. Blocked port 53?
[Tips and Tricks](https://docs.pi-hole.net/docker/tips-and-tricks/)