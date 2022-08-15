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
