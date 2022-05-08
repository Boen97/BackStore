```java
public static NewThread createAndStart() {
    NewThread t = new NewThread();
    t.t.start();
    return t;
}
```

> the key to utilizing Java's multithreading features effectively is to think **concurrently rather than serially**

> if you create too many threads, you can actually degrade the performance of your program.
> **some overhead is associated with context switching**
> more CPU time will be spent changing contexts than executing your program

> to create **compute-intensive applications that automatically scale to make use of the available processors**
> consider using the **Fork/Join Framework**
