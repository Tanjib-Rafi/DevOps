**System call to create a file**  
`open()` with the `O_CREAT` flag — it’s preferred over the old `creat()` system call because `open()` is more flexible, supports more flags, and avoids unnecessary truncation unless explicitly requested.

| Syscall  | What it does |
|----------|--------------|
| read     | Reads data from a file descriptor into a buffer. |
| write    | Writes data from a buffer to a file descriptor. |
| open     | Opens a file and returns a file descriptor (can also create files with flags like `O_CREAT`). |
| close    | Closes an open file descriptor, freeing resources. |
| fork     | Creates a new process by duplicating the calling process. |
| exec     | Replaces the current process image with a new program. |
| connect  | Initiates a connection on a socket to a remote address. |
| accept   | Accepts an incoming connection on a listening socket. |
| stat     | Retrieves metadata (size, permissions, timestamps) about a file. |
| ioctl    | Performs device-specific input/output operations on a file descriptor. |
| mmap     | Maps files or devices into memory, enabling file access via memory. |
| brk      | Changes the end of the data segment (heap), controlling heap size. |
| sbrk     | Increments or decrements the program’s data segment (heap) size. |
