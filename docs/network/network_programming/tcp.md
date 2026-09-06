# TCP programming

Based on [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/pdf/bgnet_usl_c_1.pdf)

## What is a sockets?

Way to speak to other programs using standard Unix file descriptors

A file descript - an integer associated with an open file. That file can be a network connection, a FIFO, a pipe, a terminal, a real on-the-disk file or just about anything else. Everything in Unix is a file.

### Where do I get this file descriptor for network communication?

You make a call to the `socket()` system routine. It returns the socket descriptor, and you communicate through it using the specialized `send()` and `recv()` socket calls.

### Two main types of Internet Sockets
- Stream Sockets - telnet, ssh, tcp - reliable two-way connected communication streams (error-free, arrive in the same order)
- Datagram Sockets - UDP - User Datagram Protocol, tftp, dhcpcd, multiplayer games, streaming audio etc (used due to speed) - connectionless, unreliable, if it arrives, the data withing the packet will be error-free


## Byte Order (3.2)

- Big-Endian - Network Byte Order
- Little-Endian - Host Byte Order

- short - two bytes
- long - four bytes

- htons() - host to network short
- htonl() - host to network long
- ntohs() - network to host short
- ntohl() - network to host long

## Structs

socket descriptor is int

### addrinfo
<netdb.h>
https://man7.org/linux/man-pages/man3/getaddrinfo.3.html
- struct getaddrinfo
- ai_flags


<bits/socket.h>
https://man7.org/linux/man-pages/man0/sys_socket.h.0p.html
- ai_family  AF_INET  2



<bits/socket_type.h>
https://man7.org/linux/man-pages/man2/socket.2.html
- ai_socktype  SOCK_STREAM = 1,

<netinet/in.h>
https://man7.org/linux/man-pages/man0/netinet_in.h.0p.html
- ai_protocol   IPPROTO_TCP = 6,


### System Calls or Bust

#### `getaddrinfo()`

https://man7.org/linux/man-pages/man3/getaddrinfo.3.html

It helps set up the structs you need later on.
It does all kinds of good stuff for you, including DNS and service name lookups, and fills out the structs you need


#### `socket()`

https://man7.org/linux/man-pages/man2/socket.2.html

AF - address family
PF - protocol family

```c
int s;
struct addrinfo hints, *res;

// do the lookup
// [pretend we already filled out the "hints" struct]
getaddrinfo("www.example.com", "http", &hints, &res);

// again, you should do error-checking on getaddrinfo(), and walk
// the "res" linked list looking for valid entries instead of just
// assuming the first one is good (like many of these examples do).
// See the section on client/server for real examples.
s = socket(res->ai_family, res->ai_socktype, res->ai_protocol);
```

`socket()` simply returns to you a socket descriptor that you can use in later system calls, or `-1` on error. The global varaible `errno` is set to the error's value.