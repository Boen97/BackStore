# Introducing Classes
> the class defines the shape and nature of an object.
> it forms the basis for object-oriented programming.

## Class Fundamentals

> a class defines a **new data type**
> a class is a **template** for an object.
> an object is an **instance** of a class.

### The General form of a Class.

1. the data it contains
2. the code that operates on that data.

> a class's code defines the interface to its data.

> **instance variables**
: the data or variables defined within a class

> **methods**

> **members**
: the methods and variables defined within a class are called **members of the class**

- variables defined within a class called **instance variables**
- because each instance of the class contains its own copy of these variables.

### Declaring Objects.

> `Box mybox = new Box()`
1. Box mybox // declare referencet to object
2. mybox = new Box() // allocate a object

> new allocates memory for an object during run time.
> you program can create as many or as few objects as it need.
> if unsufficient memory when new object, a run-time exception will occur.

### Introducing Methods.

- if method does not return a value, its return type must be **void**

> when method in a class is executed, the Java run-time system transfers control to the code defined inside the method.
> after the statements inside the method have executed, control is returned to the calling routine
> and execution resumes with the line of code following the call.

> **in most general sense, a method is Java's way of implementing subroutines.**

> when an instance variable is accessed by code that is not part of the class in which that instance variable is defined,
> it must be done through an object, by use of the dot operator.

> when an instance variable is accessed by code that is part of the same class as the instance variable, that variable can be referred to directly.

> parameters allow a method to be generalized.

> **parameter and argument**

1. parameter
   : a parameter is a variable defined by a method that receives a value when the method is called.
   : int m(int i) {} // i is a parameter

2. argument
   : an argument is a value that is passed to a method when it is invoked.
   : m(100) 100 is an argument

### Constructors

> allow objects to initialize themselves when they are created.
> a constructor initializes an object immediately upon creation.
> once defined, the constructor is automatically called when the object is created, before the new operator completes.

> constructor no return type, not even void.
> because the implicit return type of a class's constructor is the class type itself.

> it is the constructor's job to initialize the internal state of an object
> so that the code creating an instance will have a fully initialized, useable object immediately.

> when you do not explicitly define a constructor for a class, then Java creates a default constructor for the class.

> when using the default constructor, all non-initialized instance variables will have their default values.
> which are zero, null, and false.
> once you define your own constructor, the default constructor is no longer used.

### The this Keyword.

> **this** can be used inside any method to refer to the current object.

#### instance variable hiding

> it is illegal in Java to declare two local variable with the same name inside the same or enclosing scopes.

> when a local variable has the same name as an instance variable, the local variable hides the instance variable

> you can use this to solve any namespace collisions.

## Garbage Collection.
