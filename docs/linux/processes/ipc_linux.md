# IPC in Linux

- [IPC Linux](https://tldp.org/LDP/tlk/ipc/ipc.html)
- [Unix IPC](https://stackoverflow.com/questions/404604/comparing-unix-linux-ipc)

The most common IPC mechanisms:

1. Pipe

    Useful only among processes related as parent/child. Call pipe(2) and fork(2). Unidirectional.

2. FIFO or normal pipe

    Two unrelated processes can use FIFO unlike a plain pipe. Call mkfifo(3). Unidirectional.

3. Socket and Unix Domain socket

    Bidirectional. Meant for network communication, but can be used locally too. Can be used for different protocols. There's no message boundary for TCP. Call socket(2).

4. Message Queue

    OS maintains discrete messages. See sys/msg.h.

5. Signal

    Signal sends an integer to another process. Doesn't mesh well with multi-threads. Call kill(2).

6. Semaphore

    A synchronization mechanism for multiple processes or threads, similar to a queue of people waiting for a bathroom. See sys/sem.h.

7. Shared memory

    Do your own concurrency control. Call shmget(2).

8. Shared files
9. D-BUS
