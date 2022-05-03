> MultiTasking
1. process-based
   : a process is, a program that is executing
   : a program is the smallest unit of code that can be dispatched by the scheduler
2. thread-based
   : a thread is the smallest unit of code that can be dispatched
   : a single program can perform two or more threadss simultaneously

> process-based multitasking deals with the big picture
> thread-based multitasking handles the details

> thread requires less overhead than multitasking processes.
> processes are heavyweight require their own separate address spaces.
> interprocess communication is expensive and limited
> context switching from one process to another is also costly

> threads share the same address space and the same heavyweight process.
> interthread communication is inexpensive, and context switch is lower in cost

> process-based multitasking is not under Java's direct control.
> however, multithreaded multitasking is

> multithreading enables you to write efficient programs that make maximum use of the processing power
1. keeping idle time to a minimum

## The Java Thread Model

> Java uses threads to enable the entire environment to be asynchronous

> The value of a multithreaded environment
1. single-threaded systems use an approach called **an event loop with polling**
   : in this model, a single thread of control runs in an infinite loop,
   : polling a single event queue to decide what to do next.
   : once this polling mechanism returns with, say, a signal that a network file is ready to be read.
   : then the event loop dispatches control to the appropriate event handler
   : until the event handler returns, nothing else can happen in the program
   
> in general, in a single-threaded environment, when a thread **blocks(that is, suspends execution)**
> because it is waiting for some resource, **the entire program stops running**

> the benefit of Java's multithreading is that **the main loop/polling mechanism is eliminated**
> one thread can pause without stopping other parts of your program

> In a single-core system, concurrently executing threads share the CPU
> two or more threads do not actually run at the same time, but idle CPU time is utilized

> in multicore system, it is possible for two or more threads to execute simultaneously

> **fork/join framework**
: part of Java's support for **parallel programming**

### Threads states
1. running.
2. ready to running
3. suspended
   : a running thread can be suspended
4. resumed
5. blocked
6. terminated

### Thread Priorites

> Java assigns to each thread a **priority** that determines how that thread should be treated with respect to the others

> Thread priorities are integers that specify the **relative priority** of one thread to another

> as an absolute value, a priority is **meaningless**

> a thread's priority is used to decide when to switch from one running thread to the next.
> This is called **context switch**

1. a thread can voluntarily **relinquish control**
   : this occurs when **explicitly yielding, sleeping or when blocked**
   : all other threads are examined, and the highest-priority thread that is ready to run

2. a thread can be **preempted** by a **higher-priority** thread.
   : a lower-priority thread that does not yield the processor is simply preempted- **no matter what it is doing**
   : **preemptive multitasking**

- when two threads with the **same priority** are competing for CPU cycles
  : some operating systems, threads are in **round-robin fashion**
  : for other types of operating systems, threads must **voluntarily yield control to their peers**

> Portability problems can arise from the differences in the way that operating systems context-switch threads of equal priority.
