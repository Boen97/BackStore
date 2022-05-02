> you can only specify one superclass or any subclass that you create.

## member access and inheritance

> subclass cannot access those members that superclass that have been declared as private.

## a superclass variable can reference a subclass object.

> it is the type of the reference variable, not the type of the object that it refers to
> that determines what members can be accessed.

## using super

1. call the superclass's constructor
2. access a member of the superclass that has been hidden by a member of a subclass.

> super() must always be the first statement executed inside a subclass's constructor.

## when constructors are executed

> constructors complete their execution from superclass to subclass
> this order is the same whether or not super() is used.
> if super() is not used, then the default or parameterless constructor of each superclass will be executed.

## Method Overriding

> subclass overriding superclass method
> method overriding occurs only when the names and the **type signatures** of the two methods are identical.

## dynamic method dispatch

> method overriding forms the basis for **dynamic method dispatch**
> Dynamic method dispatch is the memchanisim by which a call to an overidden method is resolved at **run-time**, rather than **compile time**
> this is how Java implements run-time polymorphism

> a superclass reference variable can refer to a subclass object.
> Java determines which version of that method to execute based upon the type of the object being referred to at the time the call occurs.
> thus, this determination is made at run time.
> when different types of objects are referred to, different versions of an overridden method will be called.
> **it is the type of the object being referred to that determines which version of an overridden method will be executed**

## Why overridden methods?

> overridden methods allows Java to support run-time polymorphism
> polymorphism is essential to object-oriented programming for one reason.
- it allows a general class to specify methods that will be common to all of its derivatives.
- while allowing subclasses to define the specific implementation of some or all of those methods.

> the ability of existing code libraries to call methods on instances of new classes
> **without recompling while maintaining a clean abstract interface is a profoundy powerful tool**

## using Abstract Classes

> when a superclass is unable to create a meaningful implementation for a method.

### abstract method
> ensure a subclass override all necessary methods.
> this methods are sometimes referred to as **subclassr responsibility**

> any class that contains one or more abstract methods must also be declared abstract
> an abstract class cannot be directly instaniated with the new operator.
> you cannot declare abstract constructors or abstract static methods.

### using final with inheritance

#### using final to prevent overiding

> methods declared as final can sometimes provides a performance enhancement.
> the compiler is free to inline calls to them because it knows they will not be overridden by a subclass

> when a small final method is called, often the Java compiler can copy the bytecode for subroutine directly inline with the compiled code
> of the calling method, thus eliminating the costly overhead associated with a method call.

> Inlining is an option only with final methods.

> Java resolves calls to methods dynamically, at run time.
> this is called **late binding**

> since **final** methods cannot be overridden, a call to one can be resolved at **compile time**
> This is called **early binding**

#### using final to prevent inheritance
> prevent a class from being inherited
> it is illegal to declare a class as both abstract and final

> beginning with JDK 17, the ability to **seal a class** was added to Java

### The Object Class
> all other classes are subclasses of Object
> a reference variable of type Object can refer to an object of any other class.
