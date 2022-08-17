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

after the `exec` in the child

a successful call to `exec` never returns

## Tip: Getting it right(Lampson's law)

Hints for computer systems design, "Get it right"
Neither abstraction nor simplicity is a substitude for getting it right.
sometimes, you just have to do the right thing.
and when you do, it is way better than the alternatives.
there are lots of ways to design APIs for process creation
however, the combination of `fork()` and `exec()` are simple and powerful.
Here, the UNIX designers simply got it right.

## Why would we build such an odd interface to what should be simple act of creating a new process

the separation of `fork` and `exec()` is essential in building a UNIX shell
because it lets the shell run code `after` the call to `fork` but `before` the call to `exec()`
call `fork` to create a new child process to run the command,
calls some variant of `exec()` to run the command, and then waits for the command to complete by calling `wait()`

## Process control and Users

`kill()` system call is used to send `signals` to a process.
`control-C` sends a `SIGINT(interrupt)` to the process(normally terminating it)
`control-z`  sends a `SIGSTP(stop)` signals to `pausing` the process in mid-execution

you can send signals to `process group`
to use this form, a process should use the `signal()` system call to `catch` various signals

it would be dangerous anyone can arbitraily send signals such as `SIGINT`
`users` can only control their own processes

## Useful tools

1. `ps`
2. `top`
   it displays the processes of the system and how much CPU and other resources they are eating up.
