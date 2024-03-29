# Introducing to Operating Systems

## what happens when a program runs?

- a runing program does one very simple things: `it executes instructions`
- the processor `fetchs` an instruction from memory
- `decodes it` (figure out which instruction it is)
- and `execute` it
- after it is done with this instruction, the processor moves on to the next instruction
- and so on, until the program finally completes

- modern processors do many things to make programs run faster
1. executing multiple instructions at once
2. issuing and completing them out of order

## Von Neumann models of computing

- `operating system(OS)`
- in charge of making sure the system operates correctly and efficiently in an easy-to-use manner


### the crux of the problem - how to virtualize resources

- we focus on the `how`:
1. what mechanisms and policies are implemented by the OS to attain `virtualization`
2. how does the OS do so efficiently
3. what hareware support is needed

- the primary way the OS does is through a general technique called `virtualization`
- the OS takes a `physical resource` such as the processor, or memory, or a disk
- and transforms it into a more general, powerful, and easy-to-use `virtual` form
- thus, we sometimes refer to the operating system as a `virtual machine`

- the OS provides APIs to allows users to use the OS feature
- a typical OS, exports a few hundred `system calls` that are available to applications
- the OS provides `standard library` to applications

- because virtualization allows many programs to run, to share the resources
- the OS is sometimes known as a `resource manager`

- another early name for the OS was the `supervisor`

### virtualizing the CPU

when multi programs runs, the system gives us a `illusion`
a illusion that the system has a very large number of virtual CPUs

`policies` are used in OS to handle different problems
such as multiple programs runs at once, which should run first?

### virtualization the memory

memory is just an array of bytes
to ready memory, we need `address` to be able to access the data

memory is accessed all the time when a program is running
a program keeps all of its data structures in memory
each instructions of the program is in memory too.
thus memory is accessed on each instruction fetch.

each process accesses its own private `virtual address space` or `address space`
which the OS somehow maps onto the physical memory of the machine

a memory reference within one running program does not affect the address space of other processes or the OS itself

### Concurrency

the problem of concurrency are no longer limited just to the OS itself
modern `multi-threaded` programs exhibit the same problems

you can think of a thread as a function within the `same memory space` as other functions
and with more than one of them active at a time.

when the shared counter is incremented, takes three instructions:
1. one to load the value of the counter from memory into a register
2. one to increment it
3. one to store it back into memory
because these three instructions do not execute `atomically(all at once)`, strange things can happen

### Persistence

in system memory, data can easily lost
as devices such as `DRAM` store values in a `volatile manner`
we need to store data `persistently`

a `hard drive` is a common for long-lived information
although `solid-state drives (SSDs)` are making headway as well

the software in the OS which manges the `disk` is called the `file system`
it is responsible for storing any `files` the user creates in disk

unlike the abstractions provided by the OS for the CPU and memory
the OS does not create a private, virtualized disk for each application
it assumed that often times, users will want to `share` information that in `files`

file operations `system calls` are routed to the `file system`

- what the OS does in order to actually write to disk.

1. the file system first figuring out where on disk this new data will reside
   and then keeping track of it in various structures the file system maintains.
   does so requires issuing `I/O requests to the underlying storage device`,
   to either read existing structures or update(write) them

write a `hard driver` is an tough and complicated process
the OS provides a standard and simply way to access devices through its system calls
thus the OS is sometimes seen as a `standard library`

for perfomance reasons, most file systems first `delay` such `writes` for a while
hoping to `batch them` into larger groups

to handle the problems of `system crashs` during writes
most file system incorporate some kind of write protocol, such as `journaling` or `copy-on-write`
carefully ordering writes to disk to ensure that if a failure occurs during the write sequence
the system can recover to reasonable state afterwards

to make different common operations efficient
file system employ many different `data structures` and `access methods`
from simple lists to `complex b-trees`

## Design Goals

finding the right set of trade-offs to building systems

1. one of the most basic goals is to build up some `abstractions`
   to make the system convenient and easy to use.

> abstractions are fundamental of everything we do in computer science

2. one goal in designing and implementing an OS is provide high `performance`
   another way to say this is our goal is to `minimize the overheads of the OS`

virtualization and makeing the system easy to use are well worth it, but not at any costs
thus we must strive to provide virtualization and other OS features without `excessive overheads`

these overheads arise in a number of forms:
1. extra time(more instructions)
2. extra space(in memory or on disk)

3. another goal will be to provide `protection` between applications
   as well as between the OS and applications

protection is at the heart of one of the main principles, which is that of `isolation`

> isolating processes from one another is the key to protection

4. the OS must also run `non-stop`, OS needs to provide `high reliability`

## Some History

> like any system built by humans, good ideas accumulated in operating system over time
> as engineers learned what was important in their design

1. early operating systems: just libraries of commonly-used functions
   one program ran at a time, as controlled by a human operator

- this mode of computing was known as `batch` processing
- as a number of jobs were set up and then run a `batch` by the operator

2. Beyond libraries: Protection

- one important aspect of this was the realization that code run on behalf of the OS was special
- it has control of devices and thus should be treated differently than normal application code.
- because, if you allown any application to read from anywhere on the disk is dangerous
- thus, implementing a `file system` as a library makes little sense, something else is needed

- thus, the idea of `system call` was invented

- instead of providing OS routines as a library (where you just make a `procedure call` to access them)
- the idea here was to add a special pair of hardware instructions and hardware state
- to make the transition into the `OS` a more formal, controlled process.

> the key difference between a system call and a procedure call is that
> a system call `transfers control into the OS` while simultaneouly raising the `hardware priviledge level`

- `user mode`
- user applications run in what is referred to as `user mode`
- which means the hardware restricts what applications can do.
- for example, an application running in user mode can't typically initiate an I/O request to the disk

- when a system call is initiated (usually through a `trap` instruction)
- the hardware transfers control to a pre-specified `trap handler`
- simultaneouly raises the priviledge level to `kenel mode`
- in kenel mode, the OS has full access to the hardware

when the OS is done servicing the request, it passes control back to the user
via a special `return-from-trap` instruction
which reverts to user mode while simultaneouly passing control back to where the application left off.

3. The Era of Multiprogramming

`multiprogramming` became commonplace due to the desire to make better use of machine resources.

this switching was important because I/O devices were slow.
having a program wait on the CPU while its I/O was a waste of CPU time.


4. The Modern Era

- the early operating system such as `DOS (the disk operating system)` didn't think memory protection was important
