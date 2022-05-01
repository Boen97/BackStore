# Operators
1. arithmetic
2. bitwise
3. relational
4. logical

## Arithmetic Operators

- when the division operator is applied to an integer type, there will be no fractional component attached to the result.

## The Modulus Operator

> returns the remainder of a division operation.
> can be applied to floating-point types as well as integer types.

```java
int x = 42;
double y = 42.25;
x % 10 = 2;
y % 10 = 2.25;
```

## Increment and Decrement

1. ++
2. --

> postfix form
- x++ // x = x + 1
- x-- // x = x - 1
- y = ++x;

> prefix form
- y = x++;

## The Bitwise Operators

> Java defines several **bitwise operators** that can be applied to the integer types: **long, int, short, char and byte**.
> these operators act upon the **individual bits** of their operands.

1. ~ bitwise NOT
2. & bitwise AND
3. | bitwise OR
4. ^ bitwise exclusive OR
5. >> shift right
6. >>> shift right zero fill
7. << shift left
8. &= AND assignment
9. |= OR assignment
10. ^= exclusive OR assignment
11. >>= shift right assignment
12. >>>= shift right zero fill assignment
13. <<= shift left assignment

### How Java stores integer values and how it represents negative numbers ?

1. all of integer types are represented by binary numbers of varying bit widths.
: `byte a = 42;` 00101010 = 2^5 + 2^3 + 2^1

> all integer types **except char** are signed integers.

> **two's complement**
- Java uses an encoding known as **two's complement**
- negative numbers are represented by inverting all of the bits in a value, then adding 1 to the result.

- for example -42
1. 42 = 00101010
2. revert all bits 11010101
3. adding 1 11010110

- -42 to 42
1. -42 = 11010110
2. revert all bits 00101001
3. adding 1 00101010

> **zero crossing**
1. why Java uses two's complement is the issue of **zero crossing**
2. byte zero = 00000000.
3. in one's complement, simply inverting all of the bits creates 11111111, which creats **negative zero**
4. **negative zero is invalid in integer math**
5. This problem is solved by using two's complement to represent negative values.
6. when using two's complement, 1 is added to the complement, producing 10000000.
7. this produces a 1 bit too far to the left to fit back into the byte value, resulting in the desired behaviour, where **-0 is the same as 0**
8. and the 11111111 is the encoding for -1.

> because Java uses two's complement to store nagative numbers
> and because all integers are signed values in Java
> **applying the bitwise operators can easily produce unexpected results.**
> for example, turning on the high-order bit will cause the resulting value to be interpreted as a nagetive number.
> **high-order bit determines the sign of an integer no matter how that high-order bit gets set**
