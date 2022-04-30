- Java is a strongly typed language.

## The Primitive Types
- Java defines eight primitive types of data
1. byte
2. short
3. int 
4. long
5. char
6. float
7. double
8. boolean
- the primitive types are also commonly referred to as **simple types**

- four groups
1. Integers
   : byte
   : short
   : int
   : long
2. Floating-point numbers
   : float
   : double
3. Characters
   : char
4. Boolean

- primitive types are not complex object, but single value
  : although Java is object-oriented, the primitive types are not
  : the reason for this is **efficiency**

- primitive types have explicit range and mathematical behavior
  : in C++ and C, the interger size are based upon execution environment
  : in Java, all data types have a strictly defined range
  : while strictly specifying the size of an interger may cause a small loss of performance
    it is necessary to achieve portability.

### Integers.

- all of interger types are signed, positive and negative values.
> **Java does not support unsiged, positive-only integers.**
- Java's designers felt that unsiged intergers were unnecessary.

> the width of an integer type should not be thought of as the amount of storage it consumes.
> 
> but rather as the behavior it defines for variables and expressions of that type.
> 
> The Java run-time environment is free to use whatever size it wants, as long as the types behave as you declared them.

#### byte.
- the smallest integer type is byte
- signed 8-bit type, range from -128 to 127
- useful when working with a stream of data from a network or file.
- useful when working with raw binary data.

#### short.
- signed 16-bit type, range from -32768 to 32767
- the least-used Java type.

#### int.
- signed 32-bit type, range from -2^31 to 2^31 - 1
> when byte and short values are used in a expression, they are promoted to int when expression is evaluated.
> **therefore, int is often the best choise when an interger is needed**

#### long.
- signed 64-bit type
- useful for those occasions where an int type is not large enough.

### Floating-Point Types.

- floating-point numbers, also known as real numbers, are used when evaluating expressions that require fractinal precision.

#### float
- the type float specifies a single-precision value that uses 32 bits of storage.
- single precision is faster on some processors and takes half as much space as double precision.
- but will become imprecise when the values are either very large or vert small.

#### double
- use 64 bits to store a value
- double precision is actually faster than single precision on some modern processors that have been optimized for high-speed mathematical calculations.
- all transcendental math functions such as sin(), cos(), and sqrt(), return double values.

### Characters
- `char` - `16-bit`
- Unicode
- the range of a char is 0 - 65535, there is no negative chars
- ASCII still ranges from 0 to 127
- char its principle use is for representing unicode charaters, also it referred to as an integer type.

### Boolean
- println display true or false

### Interger Literals
- all whole number value is an integer literal
- base 10 
- base 8 (octal) leading zero
- base 16 (hexadecimal) leading zero-x (0x or 0X)
  : 0 - 15
  : A - F (10 - 15)
- when an integer literal assign to `char` or `byte` or `short`, no error if range are valid
- `long a = 123L`

- binary literal (0b or 0B)
  : int x = ob101010
  : the binary literal makes it easier to enter values used as bitmasks

- `int x = 123_456_789;`
- `int x = 123__456__789;`
- `int x = ob1101_1011_1111;`

### Floating Point

1. standard notation
2. scientific notation

- floating-point literal in Java default to **double** precision
- append **F/f** to specify float literal
- append **D/d** to specify double literal
- **double** type consumes 64 bits of storage
- **floate** type consumes only 32 bits of storage
- hexadecimal floating point literal 0x12.2P2, using **P or p**
- `double num = 9_423_456.0;`
- `double num = 9_423_456.1_0_9;`

### Boolean Literals
- the values of `true` and `false` do not convert into any numerical representation.
- the `true` literal in Java does not equal 1

### Character Literals
- a literal charater is represented inside a pair of single quotes
- escape sequences
  : `'\''`
  : `'\n'`
- entering a charater in octal or hexadecimal
  : `'\141'`'
  : for hexadecimal, you need enter a `\u`
  : `'\u0061'`

### String Literals
```java
String a = "Hello";
String b = "two\nlines";
String c = "\" This is in quotes\"";
```
- string literals must begin and end on the same line
- begin with JDK15, Java added a **text block**, gives you more control with multiple lines of text.
- **in Java, String are actually object types**, not arrays of charaters.
- because Java implements strings as objects, Java include extensive string-handling features that are easy to use.

## Variables

> a variable is defined by **an identifier, a type and an optional initializer**
> all variable hava a **scope**, which defines their **visibility, and a lifetime**

### Declaring a Variable

> In Java, all variables must be declared before they can be used.

- `type identifier [ = value][, identifier [ = value] ...]`

```java
int a, b, c;
int e = 1, d, f = 5;
```

### The Scope and Lifetime of Variables

> Java allows variables to be declared within any block.
> a **block** is begin with an opening curly brace and ended by a closing curly brace.
> a **block** defines a **scope**
> each time you start a new block, you are creating a new scope.

> a scope determines
1. what objects are visible to other parts of your program.
2. the lifetime of those objects.

> two major scopes in Java
1. defined by a class
2. defined by a method

> method body
: method's block of code
- if method had parameters, they too are included within the method's scope.

> variables declared inside a scope are not visible to code that defined outside the scope
- the scope rules provides the foundation for encapsulation.
- a variable declared within a block is called a **local variable**

> **scopes can be nested**
- objects declared in the outer scope will be visible to code within the inner scope.

> **variable are created when their scope is entered, and destroyed when their scope is left**
> **the lifetime of a variable is confined to its scope**

> **if a variable declaration includes an initializer, that variable will be reinitialized each time the block in which it is declared is entered.**

> **although blocks can be nested, you cannot declare a variable to have the same name as one in the outer scope**
