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

## The Synchronized Statement

> imagine a class was not created by you, by a third party, and you do not have access to the source code
> you can't add synchronized keyword to the target class
> you simple put calls to the methods defined by this class inside a **synchronized block**

```
synchronized(objRef) {
    // statements to be synchronized
}
```
- objRef is a reference to the object being synchronized
> a synchronized block ensures that a call to a synchronized method that is a member of **objRef's class** occurs 
> only after the current thread has successfully entered **objRef's monitor**
