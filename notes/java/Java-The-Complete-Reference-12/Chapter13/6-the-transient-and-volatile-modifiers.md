# The transient and volatile Modifiers
## `transient`
: when an instance variable is declared as `transient`, its value need not persist when an object is stored.
```java
class T {
    transient int a; // will not persist
    int b; // will persist
}
```
- if an object of T is written to a persistent storage area, the contents of a would not be saved, but the contents of b would.

## `volatile`
> tells the compiler that the variable modified by volatile can be changed unexpectedly by other parts of your program.
> one of the situations involves multithreaded programs.
- in a multithreaded program, two or more threads share the same variable.
- for efficiency considerations, each thread can keep its own, private copy of such a shared variable.
- the real (or master) copy of the variable is updated at various times, such as when a synchronized method is entered.
- while this approach works fine, it may be inefficient at times.
- in some cases, all that really matters is that the master copy of a variable always reflects its current state.
- to ensure this, simply use `volatile`
- **tells the compiler that it must always use the master copy of a variable**
- (or at least, always keep any private copies up-to-date with the master copy)
- also, accesses to the shared variable must be executed in the precise order
