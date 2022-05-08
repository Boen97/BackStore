# Obtaining a Thread's State

- `Thread.State.getState()`

## Thread State
1. BLOCKED
- a thread that has **suspended** execution because it is waiting to accquire a lock

2. NEW
- a thread that has not begun execution

3. RUNNABLE
- a thread that either is currently executing or will execute when it gains access to the CPU

4. TERMINATED
- a thread that has completed execution.

5. TIMED_WAITING
- a thread that has suspended execution for a specified period of time,
- such as when it has called **sleep()**
- this state is also entered when a **timeout version of wait() or join()** is called

6. WAITING
- A thread that has suspended execution because it is waiting for some action to occur
- for example, it waiting because of a call to a non-timeout version of **wait()** or **join()**

> a thread's state may change after the call to **getState()**
> it does not reflect the actual state of the thread
