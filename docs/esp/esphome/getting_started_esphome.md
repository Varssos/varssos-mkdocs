# Getting started with ESPHome

It is possible to flash esp in multiple ways:

- From Home Assistant panel
- Flash from `https://web.esphome.io/`
- Setup local web page at `http://0.0.0.0:6052` with docker very similar or the same `https://web.esphome.io/`. Pros are that you don't share any yaml files with secret and you have all necesarry esphome cmd in the local container. That's how I started

## Docker compose on linux

https://esphome.io/guides/getting_started_command_line

1. Pull image
```
docker pull ghcr.io/esphome/esphome
```

2. Fill docker-compose.yaml with:
```
version: '3'
services:
  esphome:
    container_name: esphome
    image: ghcr.io/esphome/esphome
    volumes:
      - ./config:/config:rw
      - /etc/localtime:/etc/localtime:ro
    restart: always
    network_mode: host
```

3. Run docker
```
docker compose up -d
```

4. Open `http://0.0.0.0:6052` in the browser


## Prepare yaml file
1. In esphome landing page "New device"
2. Add name
3. Fill config with ssid and password in wifi section
4. Add:
```
web_server:
  port: 80
```

5. Save
6. Flash from esphome panel or with cmd:
```
esphome run --device /dev/ttyACM0 esp32-test.yaml
```

## How to flash locally from container

```
docker compose up -d
docker exec -it esphome bash
esphome run --device /dev/ttyACM0 esp32-test.yaml
```