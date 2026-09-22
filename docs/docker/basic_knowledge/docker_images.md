# Docker images

## Pull an image or a repository from a registry
```bash
docker pull ubuntu
docker pull hello-world
```

## Create an image from existing docker containers
```bash
docker commit <container_id> <image_new_name>
```

## List docker images
```bash
docker image ls
# or
docker images
```

## List docker history layers
```bash
docker history <image_name>
```
