# A Closer Lool at Methods and Classes.

## Overloading Methods.

> methods share the same name, but different parameters.
> method overloading is one of the ways that Java supports **polymorphism**

> **one interface, multiple methods**
- method overloading supports polymorphism because it is one way that Java implements the **one interface, multiple methods** paradigm.

> in practice, you should only overload closely related operations.

## overloading constructors

## a Closer look at Argument Passing

> in general, there are two ways that a computer language can pass an argument to a subroutine.
1. **call-by-value**
   : copy the value of an argument into the formal parameter of the subroutine.
   : changes made to the parameter of the subroutine have no effect on the argument.

2. **call-by-reference**
   : a reference to an argument is passed to the parameter.
   : this reference is used to access the actual argument specified in the call.
   : changes made to the parameter will affect the argument used to call the subroutine.

> although Java uses **call-by-value** to pass all arguments.
> the precise effect differs between whether a primitive type or a reference type is passed.

> when you pass a primitive type to a method, it is passed by value.

> when you pass an object to a method
> because objects are passed by reference
> when you create a variable of a class type, you are only creating a reference to an object.
> so, it is passed a copy of the reference to the method.
> **object act as if they are passed to methods by use of call-by-reference**

> when an object reference is passed to a method, the reference itself is passed by use of call-by-value.

## Recursion

> Recursion is the process of defining something in terms of itself.
> a method that calls itself is said to be recursive.

> when a method calls itself, new local variable and parameter are allocated storage on the stack,
> and the method code is executed with these new variables from the start.

> recursive versions of many routines may execute a bit more slowly than the iterative equivalent
> because of the added overhead of the additional methods calls.

> The main advantage to recursive methods is that they can be used to create clearer and simpler versions of serveral algorithms.

> when writing recursive methods, you must have an **if** statement somewhere to force the method **return** without the recursive call being executed.

## Introducing Access Control.

> **encapsulation** provides another important attribute: **access control**
> allowing access to data only through a well-defined set of methods, you can prevent the misuse of that data.

### access modifier
1. public
2. private
3. protected
4. Java also defines a default access level.

> when a member of a class is modified by public, that member can be accessed by any other code.
> when a member of a class is specified as private, that member can only be accessed by other members of its class.

> when no access modifier is used, then by default the member of a class is public within its own package,
> but cannot be accessed outside of its package.

### understanding static

> define a class member that will be used independently of any object of that class.
> instance variables declared as static are, essentially, **global variables**

> **methods declared as static have several restrictions**
1. they can only directly call other **static** methods of their class.
2. they can only directly access **static** variables of their class.
3. they cannot refer to **this** or **super** in any way.

> **static block**
- initialize static variables with a static block, get execute exactly once, when the class is first loaded.

> this is how Java implements a controlled version of **global methods and global variables**
