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

## Process Creation: A Little More Detail

> how program are transformed into processes?

1. the first thing that the OS must do to run a program is to `load` its code and any static data (e.g., initialized variables) into memory, into `the address space of the process`

programs initially reside on `disk` in some kind of `executable format`

in early (or simple) operating systems, the loading process is done `eagerly`, all at once before running the program

modern OSes perform the process `lazily`
to truly understand how lazy loading of pieces of code and data works
you have to understand the `machinery of paging and swapping` topics when we discuess the virtualization of memory

for now ,just remmeber

> the OS must do some work to get the important program bits from disk into memory

2. allocate memory for the program's `run-time stack or just stack`

once the code and static data are loaded into memory, there are a few things the OS needs to do before running the process.
some memory must be allocated for the program's `run-time stack or just stack`
for example, C program use the stack for local variables, function parameters, and return addresses
the OS allocates this memory and gives it to the process

3. the OS may also allocate some memory for the program's `heap`
in C programs, the heap is used for explicitly requested dynamically-allocated data
the heap is needed for data structures such as linked list, hash tables, trees
the heap will be small at first, as the program runs, and requests more memory via `malloc` library API
the OS may get involved and allocate more memory to the process to help satisfy such calls

4. the OS will also do some other initialization tasks, such as `input/output(I/O)`
for example, in Unix systems, each process by default has three open `file descriptors`
for standard input, output and error;these descriptors let programs easily read input from the terminal
and print output to the screen.


5. start the program running at the entry point, namely `main()`

by loading the code and static data into memory，by creating and initializing a stack
and by doing other work as related to I/O setup, the OS now set the stage for program execution
jump to the `main()` routine, the OS transfer control of the CPU to the newly-created process
thus the program begins its execution

## Process States

in a simplified view, a process can be in one of three states:

1. Running
   a process is running on a processor. this means it is executing instructions

2. Ready
   in ready state, a process is ready to run but for some reason the OS has chosen not to run it at this given moment

3. Blocked
   in the blocked state, a process has performed some kind of operation that makes it not ready to run
   `until some other event takes place`
   a common example, when a process `initiates an I/O request on disk`
   it becomes blocked and thus some other process can use the processor

`scheduled` - process from ready state to running state
`descheduled` - process from running state to ready state

when process `blocked`, the OS will keep it as such until some event occurs (such as I/O completion)

## Data Structures

like any program,  OS has some key data structures that track various relevant pieces of information
to track the state of each process, for example, the OS likely will keep some kind of `process list` for all processes
the OS must track block processes, when an I/O event completes, the OS should make sure to wake the process and ready it to run again

the `register context` will hold, for a stopped process, the contents of its registers
when a process is stopped, its registers will be saved into this memory location

process has other state

1. `initial state`
   the process is in when it is being created

2. `final state`
   the process has exited but has not yet been cleaned up
   this is called `zoombie` state
   this final state allows other processes usually the parent that created the process
   to examine the return code of the process and see if the just-finished process executed successfully
   when finished, the parent will make one `final call(e.g. wait)` to wait for the completion of the child
   and also indicate the OS that it can clean up any relevant data


## Aside: Key Process Terms

1. the `process` is the major abstraction of a running program
   at any point in time, the process can be described by its state:
   the contents of memory in its `address space`,
   the contents of CPU registers(including `program counter` and `stack pointer`)
   and information about I/O(such as open files which can be read or written)

2. the `process API` consists of calls programs can make related to processes.
   this includes creation, destruction, and other useful calls

3. process exist in one of many different `process state`
   including running, ready to run, and blocked
   different events such as getting scheduled or descheduled, or waiting for an I/O
   transition a process from one of these states to the other.

4. a `process list` constains information about all processes in the system.
   each entry is found in what is sometimes called a `process control block(PCB)`
   which is really just a structure that contains information about a specific process.
