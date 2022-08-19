# Limited Direct Execution

by `time sharing` the CPU virtualization is achieved

## challenges

in building such virtualization machinery, there are a few challenges

1. `performance`
   how can we implement virtualization without adding excessive overhead to the system

2. `control`
   how can we run processes efficiently while retaining control over the CPU
   control is particularly important to the OS, as it is in charge of resources

to do so, both hardware and operating-system support will be required
the OS will often use a judicious bit of hardware support in order to accomplish its work efficiently

## Basic Technique: Limited Direct Execution

> just run the program directly on the CPU

when the OS wishes to start a program running, it creates a process entry for it in a process list
allocates some memory, loads the program code into memory(from disk), locates its entry point (the `main`) routine
or something else, jumps to it, and starts running the user's code.

- a few problems

1. if we just run a program, how can the OS make sure the program doesn't do anything
   that we don't want it to do, while still running it efficiently

2. when we are running a process, how does the OS stop it from running and switch to another process
   thus implementing the `time sharing` we require to virtualize the CPU


## Problem #1: Restricted Operations

> Direct execution has the obvious advantage of being fast
> the program runs natively on the hardware CPU and thus executes as quickly as one would expect.

1. `user mode`
   code that runs in user mode is restricted in what it can do

2. `kernel mode`
   which the OS or kernel runs in
   in this mode, code that runs can do what it likes

user programs perform `system call` to perform some kind of priviedge operation

in `user mode` , applications do not have full access to hardware resources
in `kernel mode` the OS has access to the full resources of the machine.

some instructions to `trap` into the kernel
and `return-from-trap` back to user-mode program
as well as instructions that allow the OS to tell the hardware where the `trap table` resides in memory

the hardware needs to be a bit careful when executing a trap
in that it must sure to save enough of the caller's registers in order to be able to return correctly
when the OS issues the return-from-trap instruction

per-process has a `kenel stack`

- how does the `trap` know which code to run inside the OS?

the kenel must carefully control what code executes upon a trap


the kenel does so by setting up a `trap table` at boot time.
when the machine boots up, it does do in priviedge(kenel) mode, and runs is free to configure machine hareware
one of the first thing the OS thus does is to tell the hardware what code to run when certain exceptional events occur

the OS informs the hardware of the locations of these `trap handlers`,
usually with some kind of special instruction

once the hardware is informed, it remembers the location of these handlers until the machine is next rebooted
thus the hardware knows what to do when system calls and other events take place

to specify the exact system call, a `system-call number` is usually assigned to each system call

## Problem #2: Switching Between Processes

> there is no way for the OS to take an action if it is not running on the CPU.

if a process is running on the CPU, this means the OS is not running

> How can the OS `regain control` of the CPU so that it can switch between processes.

### A Cooperative Approach: wait for system calls

in this style, the OS trusts the processes of the system to behave reasonably.
processes that run for too long are assumed to periodically give up the CPU
so that the OS can decide to run some other task.

### A Non-Cooperative Approach: The OS takes control

without some additional help from the `hardware`, the OS can't do much at all
when a process refuses to make system calls and return control to the OS.

> the solution: `a timer interrupt`

a timer device can be programmed to raise an `interrupt` every so many milliseconds
when the interrupt is raised, the currently running process is halted,
and a pre-configured `interrupt handler` in the OS runs.
at this point, the OS has regained control of the CPU
and thus can do what it pleases: stop the current process, and start a different one.

the OS must inform the hardware of which code to run when the timer interrupt occurs.
thus, at boot time, the OS does exactly that.
second, also during the boot sequence, the OS must start the timer,
which is of course a privileged operation.

once the timer begun, the OS can thus feel safe to run user programs.

the timer can also be `turned off`, will be discussed in `concurrency`

note that the hardware has some responsibility when an interrupt occurs
to save enough of the state of the program that was used to resume the program.

## Saving and Restoring Context.

- `scheduler`
which decides whether to continue running the currently-running process
or switch to a different one.

if the decision is to made to switch, the OS then executes a low-level piece of code
which we refer to as a `context switch`

to save the context of the currently-running process,
the OS will execute some low-level assembly code to save the general purpose registers, PC
and the kernel stack pointer of the currently-running process

One simple thing an OS might to do is `disable interrupts` during interrupt processing.
doing so ensures that when one interrupt is being handled
no other one will be delivered to the CPU
disabling interrupts for too long lead to lost interrupts, which is bad.

### How long context switches take

sub-microsecond with 2- or 3-GHz processors.

## Summary

1. the CPU should support at least two modes of execution
   a restricted `user mode` and a privileged `kenel mode`

2. typical user applications run in user mode, and use a `system call` to `trap` into the kernel
   to request operating system services.

3. the trap instruction saves register state carefully, changes the hardware status to kernel mode.
   and jumps into the OS to a pre-specified destination: the `trap table`

4. when the OS finishes serving a system call.
   it returns to the user program via another special `return-from-trap` instruction.
   which reduces priviedge and returns control to the instruction after the trap that jumped into the OS.

