- basic types are `building blocks` for data structure, and are `atoms` of Go's program

- `composite types`
: the molecules created by combining the basic types in various ways.

## Four composite types
1. arrays
2. slices
3. maps
4. structs

- arrays and structs are `aggregate types`
- their values are `concatenation` of other values in `memory`

- arrays are `homogeneous`, their elements all hava the same type
- structs are `heterogeneous`
- both arrays and structs are `fixed size`
- slices and maps are `dynamic data structure` that grow as values are added

## Arrays

- an array is a `fixed-length` sequence of zero or more elements of a particular type.
- because of their length, arrays are rarely used directly in Go.
- slice which can grow and shrink, are much more versatile.

```go
var a [3]int
for i, v := range a {}
for _, v := range a {}
```

### Array literal

```go
var q [3]int = [3]int{1, 2, 3}
```

- in an array literal, if an ellipsis '...' appears in place of the length
- the array length is determined by the number of initializers.

```go
q := [...]int{1,2,3}
```

- the size of an array is part of its type, so `[3]int` and `[4]int` are different types

```go
q := [3]int{1,2,3}
q = [4]int{1,2,3,4} // compile error, cannot assign [4]int to [3]int
```

- the literal syntax is similar for arrays, slices, maps and structs


### a list of index and value pairs

```go
type Currency int
const (
    USD Currency = iota
    EUR
    GBP
    RMB
)
symbols := [...]string{USD: "$", EUR: "b", GBP: "c"}
fmt.Println(symbols[EUR])
```

- indices can appear in any order and some may omitted,
- as before, unspecified values take on the zero value for the element type.
```go
r := [...]int{99:-1}
```
: defines an array r with `100 elements`, all zero except for the last, which has value `-1`

### comparable

> if an array's element type is `comparable` then the array type is comparable too.
> so we may directly compare two arrays of that type using the `==` operator,
> which reports whether all corrosponding elements are equal

```go
a := [2]int{1,2}
b := [...]int{1,2}
a == b
```

```go
package main

import (
	"crypto/sha256"
	"fmt"
)

func main() {
	c1 := sha256.Sum256([]byte("x"))
	c2 := sha256.Sum256([]byte("X"))
	fmt.Printf("%x\n%x\n%t\n%T\n", c1, c2, c1 == c2, c1)
}
```

- when a function is called, a copy of each argument value is assigned to the corrosponding parameter variable
- so the function receives a copy, not the original.
- passing large arrays in this way can be `inefficient`
- usinng a pointer to an array is efficient

```go
func zero(ptr *[32]byte) {
    *ptr = [32][byte]{}
}
```

- arrays are still inflexible because of their fixed size
