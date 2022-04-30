# Introducing Type inference with local variables

> not long ago, a new feature called **local variable type inference** was added to Java, Beginning with JDK 10

> two important aspects of variables
1. all variables in Java must be declared prior to use
2. a variable can be initialized with a value when it is declared
3. the type of the initializer must be the same as the declared type of the variable

> there is no need to specify an explicit type for an initialized variable
> because it could be inferred by the type of its initialize

> local variable type inference offers a number of advantages:
1. streamline code
2. simplify declarations in cases in which type name is quite lengthy.
3. helpful when a type is difficult to discern or cannot be denoted (e.g. **anonymous class**)

> **var** keyword
- to use local variable type inference, **var** must be used
- **var is context-sensitive**
- **var cannot be used as the name of a class**

> you can also use **var** to declare array
`var myArray = new int[10];`

> **var** can be used to declare a variable only when that variable is initialized
```java
var counter; // wrong! Initializer required
```

> **var** can be used only to declare local variable
> it cannot be used when declaring instance variables, parameters, or return types.

## Some var Restrictions
1. only one variable can be declared at a time.
2. cannot use null as an initializer
3. the variable being declared cannot be used by the initializer expression
4. **you cannot use var with an array initializer**
5. var cannot be used as the name of a class or other reference type, including interface, enumeration, or annotation, and generic type parameter.
6. **local variable type inference cannot be used to declare the exception type caught by a catch statememt**
7. **neither lambdae expressions nor method refrences can be used as initializer**
