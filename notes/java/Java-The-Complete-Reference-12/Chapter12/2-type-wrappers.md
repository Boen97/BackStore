# Type Wrappers

> Primitive types, rather than objects, are used for the sake of performance
> using objects for these values would add unacceptable overhead to even the simplest of calculations
> **type wrappers**, classes that encapsulate a primitive type within an object

1. Double
2. Float
3. Long
4. Integer
5. Short
6. Byte
7. Character
8. Boolean

## Character
```java
    Character c = Character.valueOf('a');
    System.out.println(c.charValue());
```

## Boolean
```java
    Boolean b = Boolean.valueOf("true");
    Boolean bb = Boolean.valueOf(false);
    bb.booleanValue();
```

## The Numeric Type Wrappers
> All of the numeric type wrappers inherit the abstract class **Number**

```java
Integer i = Integer.valueOf(12);
```

### boxing
> encapsulate a value within an object
```java
Interger iOb = Integer.valueOf(100);
```

### unboxing
> extracting a value from a type wrapper
```java
int i = iOb.intValue();
```
