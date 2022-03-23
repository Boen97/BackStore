## Object-Oriented Programming
- the core of Java
- best understand the principles of OOP

### Two paradigms

> all computer languages consist of two elements: **code** and **date**
> there are two paradigms that how a program constructed
1. process-oriented model
   : a series of linear steps
   : **code acting on data**
2. object-oriented model
   : data controlling access to code.
   : organize a program around its data
   : a set of well-definded interface to the data.
   : switching the controlling entity to data （操作的主体都是对象，例如张三吃饭，张三是对象，吃饭是Code，主体一直是对象）
   
### Abstraction
> an essential element of OOP is abstraction.
> **humans manage complexity through abstraction.**
> people don't think a car as a set of individual parts, they think it is a well-defined object with its own unique behaviour.
> people can ignore the details of the car, and just drive.

**manage abstraction**
> through the use of hierarchical classifications.
- For Example
: a car is a single object
: inside the car consists of several subsystems
: each of these subsystems is made more specific units.
: you can manage the complexity of the car through the use of hierarchical abstraction

### The Three OOP Principles
> All object-oriented programming languages provide mechanism that help you implement the object-oriented model.
1. encapsulation
   : encapsulation complexity
   : everyone knows how to access it and then use it regardless of the implementation details
   : and without fear of unexpected side effect.
   : 相同的封装，让不同的实现和迭代更为简单方便
2. inheritence
   : inheritence support the concept of hierarchical classification
   : without the use of hierarchies, each object would need to define all of its characteristics explicityly.
3. polymorphism
   : polymorphism (from Greek, meaning 'many forms')
   : allow one interface to be used for a general class of actions.
   : one interface, multiple methods
   : the same interface to be used to specify a **general class of actions**
   : it is the compiler's job to select the specific action.

### First Java Program

1. source file name
   : in Java, a source file is called **compilation unit**
   : all code must reside inside a class
   : the name of the main class should match the name of the file that holds the program.
   : Java is case-sensitive
   : this convention makes it easier to maintain and organize your program.

### compiling the Program

1. `javac` the java compiler
   : `$> javac Example.java`
   : `javac` creates a file called `Example.class` that contains the bytecode version of the program.

2. `java` run the program
   : `$> java Example`

### comment style
1. multiline comment
   ```java
   /*
   */
   ```
2. singleline comment
   `//`
3. documentation comment
   ```java
   /**
   */
   ```

### for
1. i = 0
2. check if i < 10
3. execute the code
4. i++
```java
int i;
for (i = 0; i < 10; i++) {
    code
}
```

### Lexical Issues

1. Whitespace
   : In Java, whitspace includes a space, tab, newline, or form feed.
   : form feed 换页符

2. Identifiers
   : uppercase and lowercase, numbers or the underscore and dollar-sign character.
   : dollar-sign character is not intended for general use.
   : Identifiers must not start with numbers.
   : `$test`, `this_is_ok`, `a4` are valid names.
   : **beginning with JDK 9, the underscore cannot be used by itself as an identifier**

3. Separators
   : most commonly used separator are **semicolon**.
   : () parenthese
   : {} braces
   : [] brackets
   : ;  semicolon
   : ,  comma
   : .  period separate package name
   : :: colons create method or constructor reference
   : ... ellipsis variable-arity parameter
   : @ At-sign begins an anotation
   
### The Java Class Libraries

- Java is a combination of the Java language itself, plus its standard classes.
