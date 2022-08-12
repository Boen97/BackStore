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
