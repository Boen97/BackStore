# The Abstraction: The Process

> the most fundamental abstractions that the OS provides to users: the `process`

the definition of a process, informally, is quite simple: it is a `running program`
the program itself is a lifeless thing: its just sits there on the disk, a bunch of instructions
waiting to spring into action

it is the OS that takes these bytes and gets them running, transforming the program into something useful

> how to provide many CPUs?
> how can the OS provide the illusion of a nearly-endless supply of said CPUs.

the OS creates this illusion by `virtualizing` the CPU
by running one process, then stopping it and running another

the basic technique, known as `time sharing` of the CPU
allow users to run as many concurrent processes as they would like
the potential cost is performance, as each will run more slowly because the CPU is shared

to implement virtualization of the CPU
The OS will need both some low-level `machinery` and some high-level intelligence
we call the low-level machinery `mechanisms`
`mechanisms` are low-level methods or protocols that implement a needed piece of functionality
for example, `context switch`, which gives the OS the ability to stop running one and start another one
this `time-sharing` mechanisms is employed by all modern OSes

on top of these mechanisms resides some of the intelligence in the OS, in the form of `policies`
`policies` are algorithms for making some kind of decision within the OS
for example, `scheduling policy` decide which program to run

- Tips: Use `time sharing and space sharing`
- `time sharing` allowing the resource to be used for a little while by one entity
  and then a little while by another, ans so forth
- `space sharing` where a resource is divided among those who wish to use it
  for example, disk space is naturally a space shared resouce
  once a block is assigned to a file, it is normally not assigned to another file

## The Abstraction: A Process

- the abstraction provided by the OS of a running program is something we will call a `process`
- a process is simply a running program.

to understand what constitutes a process, we thus have to understand its `machine state`:
what a program can read or update when it is running?
at any time, what parts of the machine are important to the execution of this program?

1. memory

one obvious component of `machine state` that comprises a process is its `memory`
instructions lie in memory, the data that the running program reads and writes sits in memory as well.
thus the memory that the process can address (called its `address space`) is part of the process.

2. registers

many instructions explicitly read or update registers and thus clearly they important to the process

note that there are some special registers that form part of this machine state.
for example, the `program counter(PC) or instruction pointer(IP)` tell us which instruction of the program will execute next.
similary, a `stack pointer` and associated `frame pointer` are used to manage the stack for function parameters, local variables, and return addresses.

3. persistent storage devices

program often access persistent storage devices, such I/O information might include a list of the files the process has open.

### TIP: Separate Policy and Mechanism

in many operating systems, a common design paradigm is to separate `high-level policies` from their `low-level mechanisms`
you can think mechanisms as `how does an OS perform a context switch`
think policies as `which process should the OS run right now`

separating the two allows one easily to change the policies without having to rethink the mechanism
and is thus a form of `modularity`, a general software design principle

## Process API

1. Create
   create a new process to run the program you have indicated

2. Destory
   systems also provide an interface to destroy processes forcefully
   an interface to halt a runaway process is quite useful

3. Wait
   it is useful to wait for a process to stop running

4. Miscellaneous control
   other than killing or waiting for a process, there are other controls
   for example, `suspend` a process (stop it from running for a while)
   and then `resume` it (continue it running)

5. Status
   interfaces to get some status information about a process
   such as how long it has run for, or what state it is in.
