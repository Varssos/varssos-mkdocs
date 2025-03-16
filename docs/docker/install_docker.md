# Install docker

## Install docker on ubuntu

### Follow tutorial how to install on ubuntu
https://docs.docker.com/engine/install/ubuntu/

### Encountered problems
- Permission denied for socket
```
$ docker --version
docker pull ubuntu
Docker version 28.0.1, build 068a01e
Using default tag: latest
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.48/images/create?fromImage=ubuntu&tag=latest": dial unix /var/run/docker.sock: connect: permission denied
```

1. Check if docker service runs, start and enable otherwise
```
systemctl status docker
sudo systemctl start docker
sudo systemctl enable docker
```

2. Add user to the docker group
```
sudo usermod -aG docker $USER
newgrp docker
```

3. Check socket file
```
$ ls -la /var/run/docker.sock
srw-rw---- 1 root docker 0 Mar 16 20:04 /var/run/docker.sock
```

4. Verify that the installation is successful by running the `hello-world` image:
```
sudo docker run hello-world
```
