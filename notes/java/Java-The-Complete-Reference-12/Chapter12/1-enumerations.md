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

> all enumerations automatically contain two predefined methods values() and valueOf()
`public static enum-type[] values()`
`public static enum-type valueOf(String str)`
```java
Apple[] values = Apple.values();
Apple One = Apple.valueOf("One");
for (Apple a : Apple.values()) {
}
```

## Java Enumerations Are Class Types
> the fact that enum defines a class gives the Java enumeration more power.
> for example, you can give them constructors, add instance variables and methods, and even implement interfaces

> **each enumeration constant is an object of its enumeration type**
- thus, when you define a constructor for an enum, the constructor is called when each enumeration constant is created
- each enumeration constant has its own copy of any instance variables defined by the enumeration
```java
package com.rhyme.app.test5;

public enum TestEnumeration {
  One(10),
  Two(20),
  Three(30);

  private int price;

  TestEnumeration(int price) {
    this.price = price;
  }

  int getPrice() {
    return price;
  }
}
```
> the constructor of enumeration is called once for each constant

### multi overloaded constructors
```java
package com.rhyme.app.test5;

public enum TestEnumeration {
  One(10),
  Two(20),
  Three(30),
  Four;

  private int price;

  TestEnumeration(int price) {
    this.price = price;
  }

  TestEnumeration() {
    price = -1;
  }

  int getPrice() {
    return price;
  }
}
```

### two restrictions that apply to enumerations
1. an enumeration can't inherit another class
2. an enum cannot be a superclass
> the key to remmeber 
> each of the enumeration constants is an object of the class in which it is defined

## Enumerations Inherit Enum
> all enumerations automatically inherit **java.lang.Enum**
1. **ordinal value**, begin at zero
- `final int ordinal()`

2. compare the ordinal value of two constants 
- `final int compareTo(enum-type e)`

3. **equals()**
- equality an enumeration constant with any other object
- those two objects will be equal only if they both refer to the same constant within the same enumeration
