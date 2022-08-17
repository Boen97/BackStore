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

## the exec() system call

this system call is useful when you want to run a progarm that is different from the calling program.

it does not create a new process, rather it transforms the currently running program into a different running program.

## Tip: Getting it right(Lampson's law)

Hints for computer systems design, "Get it right"
Neither abstraction nor simplicity is a substitude for getting it right.
sometimes, you just have to do the right thing.
and when you do, it is way better than the alternatives.
there are lots of ways to design APIs for process creation
however, the combination of `fork()` and `exec()` are simple and powerful.
Here, the UNIX designers simply got it right.
