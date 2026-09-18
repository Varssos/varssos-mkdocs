# Android useful cmds

## List and debug HIDL HALs
```
lshal
```


## List all processes
```
ps -ef | grep APP_NAME
```


## Check logs for xyz
```
logcat | grep -i xyz
```

## List all sockets
```
netstat -an
```

## Create local unix domain socket and send/receive data
```
nc -lUs /dev/socket/abc
```

## Connect to existing unix domain socker and send/receive data
```
nc -U /dev/socker/abc
```