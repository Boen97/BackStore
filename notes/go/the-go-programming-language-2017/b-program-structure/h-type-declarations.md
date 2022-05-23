# Type Declarations

> the type of a variable or expression defines the characteristics of the values it may take on.

- a `type` declaration defines a new `named type` that has the same `underlying type` as an existing type.
- the named type provides a way to separate different and perhaps incompatible use of the underlying type 
- so that they can't be mixed unintentionally.

- `type name underlying-type`

- type declarations most often appear at package level.

```go
package main

type Celsius float64
type Fahrenheit float64

const (
	AbsoluteZeroC Celsius = -273.15
	FreezingC     Celsius = 0
	BoilingC      Celsius = 100
)

func CToF(c Celsius) Fahrenheit {
	return Fahrenheit(c * 9 / 5 + 32)
}

func FToC(f Fahrenheit) Celsius {
	return Celsius((f - 32) * 5 / 9)
}
```

- distinguishing the types makes it possible to avoid errors like inadvertently combining temperatures in the two different scales.
- `Celsius()` and `Fahrenheit()` are conversions, not function calls
- they don't change the value or representation in any way
- but they make the change of meaning explicit

- for every type `T`, there is a corresponding conversion operation `T(x)` that converts the value `x` to type `T`
- a conversion from one type to another is allowed if both have the same underlying type
- or if both are unnamed pointer types that point to variables of the same underlying type.
- these conversions change the type but not the representation of the value.

- in any case, a conversion never fails at run time.

- the underlying type of a named type determines its structure and representation
- and also the set of intrinsic operations it supports

- comparison like `==` and `<` can also be used to compare a value of a named type
- to another of the same type
- or to a value of an unnamed type with the same underlying type.
- but two values with different named types cannot be compared directly.

```go
var c Celsius
var f Fahrenheit
c == 0 // true
f >= 0 // true
c == f // compile error: type mismatch
c == Celsius(f) // true
```

- a named type may provide notational convenience if it helps avoid writing out complex types over and over again.

- Named types also make it possible to define new behavious for values of the type through `type's methods`

- `func (c Celsius) String() string { return fmt.Sprintf("%g°C", c) }`
- `(c Celsius)` before function name
- many types declare a `String` method of this form
- because it controls how values of the type appear when printed as a string by the `fmt` package
