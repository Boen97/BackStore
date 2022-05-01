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

### The Bitwise Logical Operators
> & | ^ ~

- ^ XOR
- | OR

| A  | B  | A|B  | A&B  | A^B  | ~A  |
|:--|:--|:--|:--|:--|:--|
| 0  | 0  | 0  | 0  | 0  | 1  |
| 1  | 0  | 1  | 0  | 1  | 0  |
| 0  | 1  | 1  | 0  | 1  | 1  |
| 1  | 1  | 1  | 1  | 0  | 0  |

#### The Bitwise XOR

> the bit pattern is inverted whereever the second operand has a 1 bit
> if the second operand has a 0 bit, the first operand is unchanged.

 00101010 
^00001111
=00100101 

### The Left Shift

> for each shift left, the high-order bit is shifted out(and lost), and zero is brought in on the right.
> when a left shift is applied to an int operand, bits are lost once they are shift past bit position 31.
> if the operand is a long, then bits are lost after bit position 63.

> Java's automatic type promotions produce unexpected results when you are shifting **byte** and **short** values.
1. **byte** and **short** values are promoted to **int** when an expression is evaluated.
2. the outcome of a left shift on a **byte** or **short** value will be an **int**
3. and the bits shifted left will not be lost until they shift past bit position 31.
4. **futhermore, a negative byte or short value will be sign-extended when it is promoted to int**
5. Thus, the high-order bits will be filled with 1's.
6. **to perform a left shift on a byte or short implies that you must discard the high-order bytes of the int result**
7. for example, if you left-shift a byte value, that value will be promoted to int and then shifted.
8. this means that you must discard the top three bytes of the result if what you want is the result of a shifted byte value.
9. **the easiest way to do this is to simply cast the result back into a byte**

```java
byte a = 64, b;
int i;
i = a << 2; // 256
b = (byte) (a << 2); // 0
```

> since each left shift has the effect of doubling the original value.
> programmers frequently use this fact as an efficient alternative to multiplying by 2.

> **But you need to watch out, if you shift a 1 bit into the high-order position(bit 31 or 63), the value will become negative.**

### The Right Shift.

> When a value has bits that are shifted off, those bits are lost.
> each time you shift a value to the right, it divides that value by two-and discard any remainder.

> **sign extension**
- when you are shifeing right, the top(leftmost) bits exposed by the right shift are filled in with the previous contents of the top bit.

11111000 -8
>> 1
11111100 -4

> **if you shift -1 right, the result always remains -1, since sign extension keeps bringing in more ones in the hight-order bits**

### The Unsigned Right Shift.

> if you are shifing something that does not represent a numberic value
> you may not want sign extension to take place.
> **This situation is common when you are working with pixel-based values and graphics.**
> In these cases, you will generally want to shift a zero into the high-order bit no matter what its initial value was.

> **unsigned shift >>>**
: which always shifts zeros into the high-order bit.

- int a = -1; // 11111111_11111111_11111111_11111111
- >>> 24
- 00000000_00000000_00000000_11111111 // 255

> **>>> operator only meaningful for 32-and 64-bit values**
- smaller values are automatically promoted to int in expressions.
- **sign extension that could happend when a byte was promoted to int before unsigned shift right.** 

### Bitwise Operator Compound Assignments

a = a << 4;
a <<= 4;

## Relational Operators

> In Java, true and false are nonnumeric values that do not relate to zero or nonzero.

## Boolean Logical Operators
1. & logical AND
2. | logical OR
3. ^ logical XOR
4. || short-circuit OR
5. && short-circuit AND
6. ! logical unary NOT
7. &= AND assignment
8. |= OR assignment
9. ^= XOR assignment
10. == equal to
11. != not equal to 
12. ?: Ternary If-then-else

- &, |, ^ operate on boolean values in the same way on the bits of an integer.

### Short-Circuit Logical Operators.
> || &&
> Java will not bother to evaluate the right-hand operand when the outcome of the expression can be determined by the left operand alone.

### The Assignment Operator

> allows you to create a chain of assignments.
- int x, y, z;
- x = y = z = 100; // set x, y, and z to 100
- **the = is an operator that yields the value of the right-hand expression**
- the value of z = 100 is 100

### The ? Operator
> **ternary (three-way) operator** replace of **if-then-else** statememts

- **expression1 ? expression2 : expression3**
: expression1 evaluates to a boolean value.
: both expression2 and expression3 are required to return the same type, which can't be **void**
