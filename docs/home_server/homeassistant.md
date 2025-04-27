# Homeassistant

## Encountered problems
### Bad Gateway 502
nginx proxy manager was in different docker network
```
docker network inspect compose_default
# but homeassistant was in
docker network inspect host
```

Solution:
In NPM(Ngin Proxy Manager) use http and hostname from duckdns

### Extra actions to run with https via nginx proxy manager

1. Check nginx proxy manager ip address
```
docker network inspect compose_default
# In my case:
172.18.0.2/16
```


2. Append to config

nano /opt/docker/data/homeassistant/data/configuration.yaml

```
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 172.18.0.2
```
