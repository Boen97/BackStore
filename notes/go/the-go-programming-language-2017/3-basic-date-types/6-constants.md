# Constants

> constants are expressions whose value is known to the compiler
> and whose evaluation is guaranteed to occur at `compile time`, not at `run time`

- the `underlying` type of every `constant` is a `basic type`: boolean, string or number

```go
const (
    a = 1
    b = 2
)
```

- computations on constants can be completely evaluated at compiler time
- reducing the work necessary at run time and enabling other compiler optimizations

- `errors` ordinariily detected at run time can be reported at `compile time`
- when their operands are `constants` 
- such as integer division by zero.
- string indexing out of bounds
- and any floating-point operation that would result in a non-finite value.

```go
const IPv4Len = 4
var p [IPv4Len]byte
```

```go
const (
    a = 1 // 1
    b // 1
    c = 2 // 2
    d //2
)
```

## The constant Generator iota

- a constant declaration may use the `constant generator iota`
- which is used to create a sequence of related values without spelling out each one explicitly
- in a `const` declaration, the value of `iota`  begins at zero, and increments by one for each item.

### enumerations or enums

```go
type Weekday int
const (
    Sunday Weekday = iota
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday
)
type Flags uint
const (
    FlagUp Flags = 1 << iota // 1 << 0
    FlagBroadcast // 1 << 1
)
```

### untyped constants

- many constant are not committed to a particular type.
- the compiler represents these `uncommitted` constants with much greater numeric precision 
- than values of basic types, and arithmetic on them is more precise that machine arithmetic

- there are six flavor of these `uncommitted constants`
1. untyped boolean 
2. untyped integer
3. untyped rune
4. untyped floating-point
5. untyped complex
6. untyped string

```go
const (
    _ = 1 << (10 * iota)
    KiB // 1024
    MiB // 1048576
    GiB // 1073741824
    TiB // 1099511627776 (exceeds 1 << 32)
    PiB // 1125899906842624
    EiB // 1152921504606846976
    ZiB // 1180591620717411303424 (exceeds 1 << 64)
    YiB // 1208925819614629174706176 
)
```

- untyped constants not only retain their higher precision until later.
- but they can participate in many more expressions that committed constants without requiring `conversions`
- for example, the values `ZiB` and `YiB` in the example above are `too big` to store in any integer variable
- but they are `legitimate constants` that may be used in expressions like this one:

```go
YiB/ZiB // 1024
```

- If math.Pi had been committed to a specific type such as float64, the result would not be as precise, 
- and type conversions would be required to use it when a float32 or complex128 value is wanted:

```go
const Pi64 float64 = math.Pi
const x float32 = float32(Pi64)
```

#### for literals, syntax determines flavor

- the literal 0, 0.0, 0i, and '\u0000' all denote constants of the `same value` but `different flavors`:
1. untyped integer
2. untyped floating-point
3. untyped complex
4. untyped rune
- similarly, `true and flase` are untyped booleans
- and string literal are untyped strings

```go
var f float64 = 212
(f-32) * 5 / 9
(5 / 9 * (f - 32)) // 5 / 9 is an untyped integer
(5.0 / 9.0 * (f - 32)) // 5.0 / 9.0 is an untyped float
```

> only constants can by untyped

```go
var f float64 = 3 + 0i // untyped complex to float64
f = 2 // untyped integer to float64
f = 1e123 // untyped floating-point  to float64
f = 'a' // untyped rune to float64
```

- Whether implicit or explicit, converting a constant from one type to another requires that the target type can represent the original value.

- In a variable declaration without an explicit type (including short variable declaration)
- the flavor of the untyped constant implicitly determines the default type of the variable

```go
i := 0 // untyped integer, implicit int(0)
i := '\000' // untyped rune implicit rune('\000')
i := 0.0 // untyped floating-point implicit float64(0.0)
i := 0i // untyped complex implicit complex128(0i)
```

- Note the `asymmetry`;
1. untyped integers are converted to int, whose size is not guaranteed
2. but untyped floating-point and complex numbers are converted to the explicitly sized types float64 and complex128. 
