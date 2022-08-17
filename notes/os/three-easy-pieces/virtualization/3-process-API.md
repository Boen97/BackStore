# Process API

- in UNIX, you can create a new process with a pair of system calls: `fork()` and `exec()`
- `wait()` can be used by a process to wait for a process it has created to complete

## the fork() system call

- `PID (process identifier)`

`fork()` start from the call place, create a child process, execute the remaining instructions

## the wait() system call

it is quite useful for a parent to wait for a child process to finish what it has been doing.
this task is accomplished with the `wait()` system call (or its more completesibling `waitpid()`)

the parent process calls `wait()` to delay its execution until the child finished executing
when the child is done, `wait()` returns to the parent
