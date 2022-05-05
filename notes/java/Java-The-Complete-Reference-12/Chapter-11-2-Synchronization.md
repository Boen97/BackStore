# Synchronization

> ensure shared resource will be uesed by only **one thread at a time**
> key to synchronization is the concept of the **monitor**
> **a monitor is an object that is used as a mutually exclusive lock**
> only one thread can **own a monitor at a given time**

## Using Synchronized Methods
> all objects have their own implicit monitor associated with them.
> to enter an object's monitor, just call a method that has been modified with the **synchronized** keyword

> **race condition**
> **serialize** access to call()

> any time that you have a method, or group of methods, that manipulates the **internal state of an object** in a **multithreaded** situation.
> you should use **synchronized** keyword
> once a thread enters an **synchronized** method on an instance
> no other thread can enter any other synchronized method on the same instance
