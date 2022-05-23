> it's all `bits` at the bottom, of course,
> but computers operate fundamentally on fixed-size numbers called `words`
> which are interpreted as integers, floating-point numbers, bit sets, or memory address
> then combined into larger aggregates that represent packets, pixels...

> Go's types fall into four categories:
1. basic types 
   : numbers
   : strings
   : booleans
2. aggregate types
   : arrays
   : structs - form more complicated data types by combining values of several simpler ones.
3. reference types
   : reference typs are a diverse group that includes pointers, slices, maps, functions and channels
   : they all refer to program variables or state indirectly 
   : so that the effect of an operation applied to one reference is observed by all copies of that reference
4. interface types


## Integers

- Go provides both signed and unsigned integer arthmetic.
- four signed integers - 8, 16, 32, 64 bits - int8, int16, int32, int64
- unsigned versions - uint8, uint16, uint32 and uint64

### int and uint16

- there are two types called just `int` and `uint` 
- that are the natural or most efficient size for signed and unsigned integers on a particular platform.
- `int` is by far the most widely used numeric type.
- both these types have the same size, either 32 or 64 bits
- different compilers may make different choices even on identical hardware.

### rune

- the type `rune` is a `synonym` for `int32` and conventionally indicates that a value is a `Unicode code point`
- the two names may be used interchangeably

### byte

- the type `byte` is a `synonym` for `uint8`
- and emphasizes that the value is a piece of raw data rather than a small numeric quantity.

### uintptr

- an unsigned integer type `uintptr`
- whose width is not specified but is sufficient to hold all the bits of a `pointer value`.
- the `uintptr` type is used only for `low-level` programming
- such as at the boundary of a Go program with a C library or an operating system.

### different types

- regardless of their size, `int`, `uint` and `uintptr` are different types from their explicitly sized siblings
- `int` is not the same type as `int32`, even if the natural size of integers is 32 bits.
- and an explicit conversion is required to use an `int` value where an `int32` is needed.

### ranges

- signed numbers are represented in 2's-complement form.
- the high-order bit is reserved for the sign of number and the range of values of an n-bit number is from `-2^(n-1)` to `2^(n-1) - 1`

- unsigned numbers range `0` to `2^n - 1`
- `int8` -128 to 127
- `uint8` 0 to 255

### Binary Operators

- the remainder operator `%` applies only to `integers`
- in Go, the sign of the remainder is always the same as the sign of the dividend.
- so `-5%3` and `-5%-3` are both `-2`

- the behaviour of `/` depends on whether its operands are integers.
- so `5.0/4.0` is `1.25`, but `5/4` is 1 because integer devision truncates the result toward zero.


### overflow

- if the result of an arithmetic operation, whether signed or unsigned
- has more bits than can be represented in the result type, it is said to `overflow`
- the hign-order bits that do not fit are silently discarded.
- if the original number is a signed type
- the result could be negative if the leftmost bit is a `1`, as in the `int8` example here.
```go
var u uint8 = 255
u // 255
u + 1 // 0
u * u // 1
var i int8 = 127
i // 127
i + 1 // -128
i * i // 1
```

### binary comparison operators

- two integers of the same type may be compared using comparion operators
```go
== 
!=
<
<=
>
>=
```
- all values of the basic type - boolean, number, and strings are `comparable`
- integers, floating-point numbers, and strings are `ordered` by the comparison operators.


### unary addition and subtraction operators

- `+x` is a shorthand for `0+x`
- `-x` is a shorthand for `0-x`
- for floating-point and complex numbers, `+x` is just `x`, and `-x` is the negation of `x`

### bitwise binary operators

- `&` bitwise AND
- `|` bitwise OR
- `^` bitwise XOR
- `&^` bit clear (AND NOT)
- `<<` left shift
- `>>` right shift

- `^` is XOR when used as a binary operator
- when used as a unary prefix operator, it is bitwise negation or complement, that is, it returns a value with each bit in its operand inverted.

- `&^` 
- `z = x &^ y`
- each bit of `z` is 0 if the corresponding bit of `y` is 1
- otherwise it equals the corresponding bit of `x`

```go
var x uint8 = 1<<1 | 1<<5
fmt.Printf("%08b\n", x)    // "00100010", the set {1, 5}
```

- `%b` verb to print a number's binary digits
- `08`modifiers `%b` to pad the result with zeros to exactly `8` digits

- the shift operation and `x << n` and `x >> n` the `n` operand determines the number of bit positions to shift
- and `n` must be unsigned
- the `x` operand may be unsigned or signed
- arithmetically, a left shift `<<` is equivalent to multiplication by `2^n` 
- a right shift `>>` is equivalent to the floor of division by `2^n`


- Left shifts fill the vacated bits with zeros, as do right shifts of unsigned numbers, 
- but right shifts of signed numbers fill the vacated bits with copies of the `sign bit`
- for this reason, it is important to use unsigned arithmetic when you're treating an integer as a bit pattern.

### why use signed int form even for quanties that can't be negative?

- Although Go provides unsigned numbers and arithmetic, 
- we tend to use the signed int form even for quanties that can't be nagative
- such as the length of an array.
- though `uint` might seem a more obvious choice.

```go
medals := []string{"a", "b", "c"}
for i := len(medals) - 1; i >= 0; i-- {
    fmt.Println(medals[i])
}
```

- If len returned an unsigned number, 
- then `i` too would be a `uint`
- and the condition `i >= 0` woudl always be `true` by definition
- After the third iteration, in which i == 0, the i-- statement would cause i to become not −1, but the maximum uint value (for example, 264−1),
- the evaluation of medals[i] would fail at run time
- for this reason, unsigned numbers tend to be used only when their bitwise operators or 
- peculiar arthmetic operators are required, as when implementing bit sets, parsing binary file formats, or for `hashing and cryptography`
- **they are typically not used for merely non-negative quanties**

```go
var apples int32 = 1
var oranges int64 = 2
var compote int = applies + oranges // compile error
```

- fix1
`var compote int = int(apples) + int(oranges)`

- many integer-to-integer conversions do not entail any change in value.
- they just tell the compiler how to interpret a value.

## narrows a big integer into a smaller one

- But a conversion that nar- rows a big integer into a smaller one, 
- or a conversion from integer to floating-point or vice versa, may change the value or lose precision:
- Float to integer conversion discards any fractional part, truncating toward zero. 
- You should avoid conversions in which the operand is out of range for the target type
- because the behav- ior depends on the implementation:

```go
f := 1e100  // a float64
i := int(f) // result is implementation-dependent
```

## integer literal

- Integer literals of any size and type can be written as ordinary decimal numbers, 
- or as octal numbers if they begin with 0, as in 0666, or as hexadecimal if they begin with 0x or 0X, as in 0xdeadbeef.
- Hex digits may be upper or lower case.

- Nowadays octal numbers seem to be used for exactly one purpose
- `file permissions on POSIX systems`
- but hexadecimal numbers are widely used to emphasize the bit pattern of a number over its numeric value.

## %d, %o and %x verbs

```go
o := 0666
fmt.Printf("%d %[1]o %#[1]o\n", o) // 438 666 0666
x := int64(0xdeadbeef)
fmt.Printf("%d %[1]x %#[1]x %#[1]X\n", x) // 3735928559 deadbeef 0xdeadbeef 0XDEADBEEF
```
-  the [1] ‘‘adverbs’’ after % tell Printf to use the first operand over and over again.
- the `#` adverb tells Printf to emit a `0` or `0x` or `0X` prefix respectively.

## Rune literals are written as a character within single quotes.

```go
ascii := 'a'
newline := '\n'
fmt.Printf("%d %[1]c %[1]q\n", ascii) // "97 a 'a'" ascii only write once
```
- Runes are printed with %c, or with %q if quoting is desired
