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