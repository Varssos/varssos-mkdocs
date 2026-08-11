# Draft notes about system programming


API - Application Programming Interface
- API is a definition
- Ensures source compatibility. Source can be compiled for different platforms, works in a specific way

ABI - Application Binary Interface
- Calling conventions, byte ordering, register use
- Ensures binary compatibility
- Defined/implemented by Kernel and toolchain

POSIX - Portable Operating System Interface
- C APIs for Unix-like operating systems


## Linux Filesystems

"Everything is A File"
- Much of the interaction with the kernel occurs via reading/writing files
- Devices are accessed similar to files /dev/ttyUSB0


Linux Inode (Index Node)
- Metadata used to track files on disk
- Includes timestamp, owner, size, mode (access permission), location
- Fixed small (128 byte) size
- Filename is not included

- Why not icnlude filesnames in Inodes?
    - Allows different file names to share the same contentwithout duplicating Inode content

- Two types of Links, Hard and Symbolid(symlinks)
    - Hard Links map directly to inodes, only allowed on the same filesystem
    - Soft links map to filenames, work across filesystems, can be broken

Linux Special files:
- Kernel objects represented as files:
    - Character Device
        - Linear queue of bytes
        - Example: Keyboard
    - Block Device
        - Array of bytes, addressable in a sector
        - IE Hard Disk
    - Named Pipes/ Sockets
        - Interprocess Communication

- Smallest unit addressable is a block
    - block is a power of two multiple of sector size
    - Typical/historical sector size is 512 bytes


## Processes and Threads
ELF - Executable and Linkable Format

- Necessary resources to run are allocated and managed by the kernel through system calls
    - Timers
    - Files
    - Hardware access 


Linux Threads
- Unit of activity within a process
- Each thread has:
    - Stack - stores local variables
    - Processor state/current location
- Memory address space is shared between threads

Linux Signals:
- One-way asynchronous notifications sent from:
    - Kernel to process
    - One process to another process (IPC)
    - A process to itself
- Process setup signal handlers to control how to respond to a signal
- Signal handlers must use signal safe functions which are safe to call asynchronously
    - Use of global variables can introduce unsafe scenatios
    - Process code can be interrupted at any time by signals
    
IPC:
- Pipes
- Semaphores
- Message Queues
- Shared Memory

## Users and Groups
- Each user is associated with a User ID (uid)
- /etc/passwd maps usernames uids
- UID 0 is the root user

- Each user belongs to one or more groups, with corresponding Group IDs (gid)
    - /etc/groups maps group names to gids

## Error handling
- C library mechanism for reporting errrors is errno
- Print error message:
    - perror("perror returned)  
    - strerror(errno)

- Wouldn't an error in one thread override an error in a second thread?
    - This is handled for us by POSICX



## Toolchains
- Compiler
- Linker
- Run-time libraries
- GCC or Clang are the most likely toolchain options

- Binutils - binary utilities including assembler and linker
- GCC - Gnu Compiler Collection
    - Compiler for programming langueges ( C in our case.)

- C Library - API based on POSIX definition

### Setting Up a Toolchain
Option 1: Do it manually by downloading/buidling/installing components yourself
Option 2: Use a build system to generate(Buildroot/Yocto)

### Types of TOolchains
- Native toolchain
    - Runs on the same system as the program it generates
- Cross toolchain
    - Runs on a different architecture than the host
    - "cross compiling"
        - creating output for a different hardware architecture

Why use a cross toolchain?
- Your host is probably more powerful than the target, builds are faster
- You probably don't want to include develeopment tools in your target image. Might not be possible to fit these in your target image

Example for QEMU: aarch64-none-linux-gnu-gcc
- CPU is ARM 64 bit
- Vendor is "none" (Support a common set of ARM CPUs)
- Kernel is "linux"
- Operating system is GNU GCC


### Sysroot, library and header files

- Sysroot is the root fielsystem of your (cross) toolchain
- Consists of files specific to the target type. Mirrors files on your host root filesystem
- Some files are needed to compile programs
- Others are (also) needed on the target at runtime

### Sysroot Directories
- lib -shared objects for C library (on target)
- usr/lib - static library archive files for the C library
- usr/include - Headers for libraries ( for instance <stdio.h>)
- usr/(s)bin - Utility programs for the cross toolchain

### Other tools in the toolchain
- Use all cross toolchain components with the same prefix referenced for gcc
- gcc, g++ - compiler
- gdb - debugger
- ld - linker

- addr2line - converts program addresses into filenames/numbers for debug
- objdump - disassemble object files
- strip - Remove debug tables, make binary files smaller
- readelf - Additional information aobut executables (object code, location in memory map, etc)

### Static vs Dynamic Linking
- gcc or g++ always links with glibc, the C library
- Static Linkage
    - All library functions and dependencies are pulled from archive and placed in your executable

- Dynamic Linkage
    - Linking is done dynamically at runtime


- When to use Static Linkage?
    - WHen you have relatively few application(or only a single application)
        - Busybox
        
    - You need to run an application before the root filesystem is available
     When would that happen?
        - At boot, loading storage drivers

- Linked checks for shared libraries in:
    - /lib, /lib64
    - /usr/lib, /usr/lib64
    - content of LD_LIBRARY_PATH


## Logging and Syslog
Syslog and syslogd is framework to store information in log files
syslogd is a daemon which:
- uses configuration file to configure logging (Usually writting to files in /var/log)
- Handles log messages from applications using syslog() API calls


```C
openlog(NULL,0,LOG_USER);
syslog(LOG_ERR,"Invalid Number of arguments: %d", argc)
```

Result in message in /var/log/syslog

Log redirection in an Ubuntu VM happens based on rules in `/etc/rsyslog.d/*default.conf`
