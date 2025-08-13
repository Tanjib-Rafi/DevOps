**System call to create a file**  
`open()` with the `O_CREAT` flag — it’s preferred over the old `creat()` system call because `open()` is more flexible, supports more flags, and avoids unnecessary truncation unless explicitly requested.
