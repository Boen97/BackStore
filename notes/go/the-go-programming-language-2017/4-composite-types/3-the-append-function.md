- the built-in `append` function appends items to slices

```go
package main

import "fmt"

func main() {
	var runes []rune
	for _, r := range "Hello, World" {
		runes = append(runes, r)
	}
	fmt.Printf("%q\n", runes)
    fmt.Printf("%q\n", []rune("Hello, World"))
}
```

## how `append` works

- the `append` function is crucial to understanding how slices work
- so let's take a look at what is going on.

```go
func appendToInt(x []int, y int) []int {
	var z []int
	zlen := len(x) + 1
	if zlen <= cap(x) {
		// there is room to grow, extend the slice.
		z = x[:zlen]
	} else {
		// there is insufficient space. allocate a new array.
		// grow by doubling, for amortized linear complexity.
		zcap := zlen
		if zcap < 2*len(x) {
			zcap = 2 * len(x)
		}
		z = make([]int, zlen, zcap)
		copy(z, x)
	}
	z[len(x)] = y
	return z
}
```

- be remmeber, `append` could will cause a reallocation

> to use slices correctly, it's important to bear in mind that 
> although the elements of the underlying array are indirect,
> the slice's `pointer`, `length`, and `capacity` are not.

> slices are not pure reference types, but resemble an aggregate type such as this struct:

```go
type IntSize struct {
    ptr *int
    len, cap int
}
```

- the built-in `append` lets us add more that one new element, or even a whole slice of them.

- `variadic function`

```go
func appendInt(x []int, y ...int) []int {
}
```
