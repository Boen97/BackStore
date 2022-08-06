# Generics

## Type Parameters

```go
func Index[T comparable](s []T, x T) int
```

```go
package main

import "fmt"

func Index[T comparable](s []T, x T) int {
	for i, v := range s {
		if v == x {
			return i
		}
	}
	return -1
}

func main() {
	ss := []string{"foo", "Rhyme"}
	fmt.Println(Index[string](ss, "Rhyme"))
}
```

- `comparable` is a useful constraint that makes it possible to use the `==` and `!=`

## Generic types

- in addition to `generic functions`
- Go also supports `generic types`

```go
package main

import "fmt"

type List[T any] struct {
	val T
}

func main() {
	l := List[string]{"Rhyme"}
	fmt.Println(l.val)
}
```
