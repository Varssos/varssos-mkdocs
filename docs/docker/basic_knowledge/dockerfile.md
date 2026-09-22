# Dockerfile

With Dockerfile you can create images using a text file called exactly `Dockerfile`

## Example Dockerfile
```dockerfile
FROM ubuntu

COPY skni.txt .

RUN apt-get update
RUN apt-get install --yes vim
```

## Create image with dockerfile
```bash
docker build <path_to_Dockerfile>
# E.g.
docker build .
```

## Create image with dockerfile and set its tag
```bash
docker build --tag <tag_name> <path_to_Dockerfile>
# E.g.
docker build --tag my_vim .
```
