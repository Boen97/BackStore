# Process API

- in UNIX, you can create a new process with a pair of system calls: `fork()` and `exec()`
- `wait()` can be used by a process to wait for a process it has created to complete

## the fork() system call

- `PID (process identifier)`

`fork()` start from the call place, create a child process, execute the remaining instructions
