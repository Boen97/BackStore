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

### Synchronization

> because multithreading introduces an **asynchronous** behavior to your programs.
> there must be a way for you to **enforce synchronicity** when you need it.
> that is, you must prevent one thread from writing data while another thread is in the middle of reading it
> for this purpose, Java implements an elegant twist on an age-old model of interprocess synchronization: the **monitor**
> **you can think of a monitor as a very small box that can hold only one thread**
> **once a thread enters a monitor, all other threads must wait until that thread exits the monitor**

> In Java, there is no class **Monitor**
> each object has its own **implicit monitor** that is automatically entered when one of the **object's synchronized method** is called
> once a thread is **inside a synchronized method**, no other thread can call any other synchronized method on the **same object**

### Messaging

> after you divide your program into separate threads.
> **you need to define how they will communicate with each other**
> if depends on the operating system to establish communication between threads. This of course, **adds overhead**
> Java provides a clean, low-cost way for two or more threads to talk to each other,
> **via calles to predefined methods that all object have**
> Java's messaging system allows a thread to enter a synchronized method on **an object**
> and then **wait there until some other thread explicitly notifies it to come out**

### The Thread Class and the Runnable Interface

> Java's multithreading system is built upon the **Thread** class, **its methods**, and **its companion interface Runnable**
> **Thread encapsulates a thread of execution**
> since you can't directly refer to the **ethereal state** of a running thread. you will deal with it through **its proxy**
> the Thread instance that spawned it.
> to create a new thread, you can **extend Thread or implement the Runnable interface**

> the Thread class defines serveral methods
1. getName
2. getPriority
3. isAlive
4. join
   : wait for a thread to terminate
5. run
   : entry point for the thread.
6. sleep
   : suspend a thread for a period of time.
7. start
   : start a thread by calling its run method

### The Main Thread
> when a Java program starts up, one thread begins running immediately.
> This is called **the main thread** of your program

> The main thread is important for two reasons:
1. it is the thread which other "child" threads will be spawned.
2. often, it must be the last thread to finish execution, because it performs various shutdown actions

> **currentThread()**
- `static Thread currentThread()`
  : this method returns a reference to the thread in which it is called.
- you can use `Thread.currentThread()` to get the reference of the main thread

- **thread group**
: is a data structure that controls the state of a collection of threads as a whole

- `Thread.sleep(1000);`
: casuse the thread from which it is called to suspend execution for the specified period of milliseconds

- static void sleep(long milliseconds, int nanoseconds) throws InterruptedException

### Creating a Thread

1. implement the Runnable Interface

2. extend the Thread class

#### Implementing Runnable

> Runnable abstracts a unit of executable code

```java
Thread(Runnable threadOb, String threadName)
```

- thread.start() initiates a call to run()

- it is often useful for the main thread to be the last thread to finish running

```java
package com.rhyme;

public class ThreadDemo {
  public static void main(String[] args) {
    NewThread newThread = new NewThread();
    newThread.t.start();
    try {
      for (int i = 5; i > 0; i--) {
        System.out.println("MainThread" + i);
        Thread.sleep(1000);
      }
    } catch (InterruptedException e) {
    }
    System.out.println("Main Thread exit");
  }
}


class NewThread implements Runnable {
  Thread t;

  NewThread() {
    t = new Thread(this, "SubThread");
  }

  @Override
  public void run() {
    try {
      for (int i = 5; i > 0; i--) {
        System.out.println("SubThread" + i);
        Thread.sleep(500);
      }
    } catch (InterruptedException e) {
    }
    System.out.println("subThread exit");
  }

}
```

### Extending Thread

```java
class NewThread extends Thread {
    public void run() {
        ...
    }
}
public static void main(String[] args) {
    Thread t = new Thread();
    t.start();
    ...
}
```

### Using isAlive() and join()

> How can one thread know when another thread has ended ?
1. `final boolean isAlive()`
2. `join()`
   : this method will wait until the thread on which it is called terminates
   : its name comes from the concept of the calling thread waiting until the specified thread **joins** it.

```java
package com.rhyme;

public class TestJoin {
 public static void main(String[] args) {
   MyThread t1 = new MyThread("Thread1");
   MyThread t2 = new MyThread("Thread2");
   MyThread t3 = new MyThread("Thread3");
   t1.t.start(); // 等待t1 加入主线程
   t2.t.start();
   t3.t.start();

   try {
    t1.t.join();
    t2.t.join();
    t3.t.join();
  } catch (InterruptedException e) {
  }
  System.out.println("Main Thread exit");
 }
}
```

### Thread Priorites

> Thread Priorites are used by the **thread scheduler** to decide when each thread should be allowed to run.
> in **theory**, over a given period of time, higher-priority threads get more CPU time that lower-priority threads
> in **practice**, depends on serveral factors:
: for example, how operating system implements multitasking
> a higher priority thread **preempt** a low-priority one.

> **threads of equal priority**
1. depends on different operating system implements
2. **threads that share the priority should yield control once in a while**

> `setPriority()`
: within **MIN_PRIORITY** and **MAX_PRIORITY**

> **NORM_PRIORITY**
: return a thread to default priority
