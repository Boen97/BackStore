# Interface

- an interface type is defined as a set of method signatures
- a value of interface type can hold any value that implements those methods

```go
package main

import "fmt"

type Hello interface {
	Hello()
}

type Rhyme struct {
	name string
}

func (r *Rhyme) Hello() {
	fmt.Println("hello", r.name)
}

func main() {
	var h Hello
	r := Rhyme{"Rhyme"}
	h = &r
    h = r//compire err, becasue only *Rhyme implements Hello interface
	fmt.Println(h)
}
```

## Interfaces are implemented implicitly

- a type implements an interface by implementing its methods

> implicit interfaces decouple the definition of an interface from
> its implementation
> which could then appear in any package without prearrangement

## Interface values

- interface values can be thought of as a tuple of a value and a concrete type

```
an interface value = (value, type)
```

- an interface value holds a value of a specific underlying concrete type

- calling a method on an interface value executes the methods on its underlying type

## Interface values with nil underlying values

- just gracefully handle nil situation in methods

```go
type I interface {
    M()
}
type T struct {
}
func (t *T) M() {
    if (t == nil) {
        return
    }
}
var i I
var t *T
i = t
i.M()
```
