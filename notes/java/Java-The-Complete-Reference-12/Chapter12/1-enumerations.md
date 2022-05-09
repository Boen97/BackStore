> an enumeration is a list of names constants that define a new data type and its legal values.
> an enumeration object can hold only a value that was declared in the list
> **an enumeration gives you a way to explicitly specify the only values that a data type can legally have.**
> example: **error codes**

> **In Java, an enumeration defines a class type**
- by making enumerations into classes, the capabilities of the enumeration are greatly expanded
- in Java, an enumeration can hava constructors, methods, and instance variables

## Enumeration Fundamentals
```java
public enum Apple {
    One,
    Two,
    Three
}
```
### **enumeration constants**
: One, Two, Three are called enumeration constants
: each enumeration constant is **implicitly declared as public, static final member of Apple**
: they are **self-typed**, their type is the type of the enumeration in which they are declared

> even though enumerations define a class type, you do not instantiat an enum with new
- `Apple ap = Apple.One`

> two enumerations can be compared for equality by using **==** 

> an enumeration value can also be used to control a **switch** statement
```java
TestEnumeration t = TestEnumeration.One;
    switch (t) {
      case One:
      case Two:
      case Three:
    }
```
- **One not Apple.One**
- **the type of the enumeration in the switch expression has implicitly specified the enum type of the case constants**
- there is no need to qualify the constants in the case statements with their enum type name.
- using enum type name will cause a compliation error.

> when an enumeration constant is displayed, such as in println(), its name is output.
```java
System.out.println(Apple.One) // One
```

### the values() and valueOf() Methods
