# Packages and Interfaces

> Packages
- container for classes
- used to keep the class name space compartmentalized.

> Interfaces
- a class can implement more than one interface

## Packages

> unique name had to be used for each class to avoid name collisions.
> Java use Packages to partitioning the class name space into more manageable chunks.
> the package is both a naming and a visibility control mechanism.

### defining a Package

> to create a package is quite easy
> simply include a **package** command as the first statement in a Java source file.
> any class declared within that file will belong to the specified package

> the package statement defined a name space in which classes are stored.
> if you emit the package statement, the class names are put into the default package, which has no name.

> Java uses file system directories to store packages.
> the directory name must match the package name exactly

> the package statement simply specifies to which package the classes defined in a file belong.
> it does not exclude other classes in other files from being part of that same package

> a package hierarchy must be reflected in the file system of your Java development system.
- package a.b.c;
- need to be stored in a\b\c
> you cannot rename a package without renaming the directory in which the classes are stored

### Finding Packages and CLASSPATH

> packages are typically mirrored by directories

> how does the Java run-time system know where to look for packages that you create?
1. by default, the Java run-time system uses the **current working directory** as its starting point.
: thus, if your package is in a subdirectory of the current directory, it will be found.

2. specify a directory path or paths by setting the **CLASSPATH** environmental variable
: the class path must not include the package itself

3. use the **-classpath** option with java and javac to specify the path to your classes

4. beginning with JDK9, a package can be part of a module, and thus found on the module path.

### Packages and Memeber Access

- Java addresses four categories of visibility for class memebers:
1. subclasses in the same package
2. non-subclasses in the same package
3. subclasses in different packages
4. classes that are neither in the same package nor subclasses

- modifiers
> only to members of classes

1. private
   : same class
2. public
   : same class
   : same package subclass
   : same package non-subclass
   : different package subclass
   : different package non-subclass
3. protected
   : same class
   : same package subclass
   : same package non-subclass
   : different package subclass
   > allow an element to be seen outside your current package, but only to classes that subclass of your class directly
4. no modifier
   : same class
   : same package subclass
   : same package non-subclass
   > visible to subclasses as well as other classes in the same package

> a non-nested class has only two possible access levels: **default and public**

> When a class is public, it must be the only public class declared in the file
> and the file must have the same name as the class.

### Importing Packages

> classes within packages must be fully qualified with their package name or names

- `import pkg1[.pkg2].(classname | *)`

> all of the standard Java SE classes included with Java begin with the name **java**
> basic language functions are stored in a package called **java.lang**
> **java.lang** is implicitly imported by the compiler for all programs.

> If a class with the same name exists in two different packages that you import using the start from,
> the compiler will remain silent, unless you try to use one of the classes.

## Interfaces

> one class can implement any number of interfaces.
> by providing the interface, Java allows you to fully utilize the **one interface, multiple methods** aspect of **polymorphism**

> Interfaces are designed to support **dynamic method resolution at run time**

> beginning with JDK8, it is possible to add a **default implementation** to an interface method
> JDK8 aslo added **static interface methods**
> beginning with JDK9, an interface can include **private methods**

> interface variables are implicitly **final** and **static**
: they cannot be changed by the implementing class, and must be initialized
> all methods and variables are implicitly **public**

### Implementing Interfaces
- **implements**
> if a class implements more than one interface, the interfaces are separated with a comma.

### Partial Implementations
> a class not fully implement the methods required by that interface, the class must be declared **abstract**

### Nested Interface

```java
class A {
    public interface NestedIF {
        void hello();
    }
}
class B implements A.NestedIF {
    public void hello() {
    }
}
```

### Variables in Interfaces

> you can use interface to import shared constants into multiple classes by simply declaring an interface that contains variables

### Interfaces Can be Extended

> One interface can inherit another by use of the keyword **extends**

### default interface methods

> from JDK8, interface support **default method or extension method**
> default method does not change a key aspect of interface: **its inability to maintain state information**
> an Interface still cannot have instance variables
> **keyword default**

### Multiple Inheritance Issues

> Java does not support multiple inheritance of classes.
> an interface can include default methods.
> if an interface can provide a way around this restriction.
> No!
> **a class maintain state information(instance variables), but an interface cannot**

> a class implementation takes priority over an interface default implementation

### Use static Methods in an Interface

### Private Interface Methods
