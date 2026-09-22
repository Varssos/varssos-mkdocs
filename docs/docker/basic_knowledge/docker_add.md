# Docker add

## Docker add, download file from link
```dockerfile
FROM ubuntu

ADD http://archive.ubuntu.com/ubuntu/pool/main/n/nano/nano_6.2-1_amd64.deb .

RUN ls
```

## Docker add, extract tar.gz
```dockerfile
FROM ubuntu

ADD test.tar.gz .

RUN ls
```
