# Stringer interface

```go
type Stringer interface {
    String() string
}
```

```go
package main

import "fmt"

type Rhyme struct {
	name string
}

func (r *Rhyme) String() string {
	return fmt.Sprint(r.name)
}

func main() {
	fmt.Println(&Rhyme{"World"})
}
```
