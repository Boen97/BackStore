> sometimes, knowing the type of an object during run time is useful.
- example 1
  : one thread generates various types of object
  : another thread process these objects.
- example 2
  : knowledge of an object's type at run time is important involves casting.
  - many invalid casts can be caught at compile time.
  - casts involving class hierarchies can produce invalid casts that can be detected only at run time.
  
> how can you know, at run time, what type of object is actually being referred to ?
- Java provides the **run-time operator instanceof** to answer this question.

> `instanceof` was significantly enhanced by JDK17 with a powerful new feature based on **pattern matching**
> `instanceof` is the means by which your program can obtain run-time type information about an object.
> it can be useful when you're writing generalized routines that operate on objects of a complex class hierarchy
> or that are created from code outside your direct control.
```java
package com.rhyme.app.test9;

public class TestInstanceof {
  public static void main(String[] args) {
    A a = new A();
    B b = new B();
    A c = b;
    System.out.println(a instanceof A); // true
    System.out.println(b instanceof A); // true
    System.out.println(c instanceof B); // true
  }
}

class A {
}

class B extends A {
}
```
