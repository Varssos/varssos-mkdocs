# Docker containers

## Create new docker container
```bash
docker run ubuntu
```

## Create new docker container with interactive bash
```bash
docker run --interactive --tty ubuntu bash
# or
docker run -it ubuntu bash
```

## Print all docker containers
```bash
docker container ls -a
# or
docker ps -a
```

## Print running docker containers
```bash
docker container ls
# or
docker ps
```

## Start again docker container
```bash
docker start <container_id>/<container_name>
```

## Execute command in running docker container
```bash
docker exec <container_id>/<container_name> ls
```

## Go to interactive mode on running docker container
```bash
docker exec -it <container_id>/<container_name> bash
```
