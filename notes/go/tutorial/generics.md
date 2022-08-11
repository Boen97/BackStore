# Getting started with generics

```go
package main

import "fmt"

func SumIntsOrFloats[K comparable, V int64 | float64](m map[K]V) V {
	var s V
	for _, v := range m {
		s += v
	}
	return s
}

func main() {
	ints := map[string]int64{
		"1": 1,
		"2": 2,
	}
	fmt.Println(SumIntsOrFloats[string, int64](ints))
    fmt.Println(SumIntsOrFloats(ints))
}
```

- you can emit type parameters in calling code when the Go compiler can infer the types

## declare a type constraint

```go
type Number interface {
    int64 | float64
}
```

```go
func SumIntsOrFloats[K comparable, V Number](m map[K]V) V {
	var s V
	for _, v := range m {
		s += v
	}
	return s
}
```
