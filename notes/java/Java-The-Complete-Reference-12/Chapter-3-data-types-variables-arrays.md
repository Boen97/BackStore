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
