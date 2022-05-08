# Suspending, Resuming, and Stopping Threads

> Prior to Java2, a program used **suspend(), resume(), and stop()**, which are methods defined by **Thread**

## Why don not use **suspend**?
> 1. deprecated
> 2. cause serious system failures.
> assume that a thread has obtain locks on critical data structures.
> if that thread is suspended at that point, **those locks are not relinquished**
> **other threads that may be waiting for those resources can be deadlocked.**

## why do not use resume()
> resume() cannot use without the suspend()

## why do not use stop()
> assume that a thread is writing to a critically important data structure and has completed only part of its changes.
> if that thread is stopped at that point, that data structure might be left in a **corrupted state**
> **the trouble is that stop() causes any lock the calling thread holds to be released**
> the corrupted data might be used by another thread that is waiting on the same lock

## new way to pause, restart, or terminate a thread
> a thread must be designed so that the **run()** method 
> periodically checks to determine whether that thread should suspend, resume, or stop its own execution
> this is accomplished by **a flog variable** that indicates the execution state of the thread
> the central theme will be the same for all programs


## use wait() and notify() to control the execution of a thread
