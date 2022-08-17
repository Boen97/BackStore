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
