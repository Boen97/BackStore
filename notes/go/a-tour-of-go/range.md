# Range

- the `range` of the `for` loop iterates over a slice or map.
- when ranging over a slice, two values returned for each iteration.
- the first is the index, the second is a `copy of the element at that index`

```go
package main

import "fmt"

type Rhyme struct {
	name string
}

func main() {
	a := []Rhyme{
		{"Rhyme"},
		{"Chiang"},
	}
	for _, v := range a {
		v.name = "Hello" // copy of the element at that index
	}
	fmt.Println(a)
}
```

- you can skip the index or value by `_`
