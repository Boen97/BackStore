# Methods

- Go does not have classes
- However, you can define methods on types.
- a method is a function with a special receiver argument.

```go
type Rhyme struct {
	name string
}
func (r Rhyme) hello() {
	fmt.Println("Hello", r.name)
}
```

- a methods is just a function with a receiver argument

## declare a method on non-struct type

- you can declare a method on non-struct types
- you can only declare a method with a receiver, whose type is defined in the same package as the method
- you cannot declare a method with a receiver whose type is defined in another package
- which includes the built-in types such as `int`

```go
package main

import "fmt"

type MyInt int

func (MyInt) helloInt() {
	fmt.Println("hello int")
}

func main() {
	var t MyInt = 2
	t.helloInt()
}
```

## Pointer receivers

- with a `value receiver`, the method operates on a copy of the original (deep copy)

- with `pointer receivers`, the receiver type has the `*T`
- `T` cannot itself be a pointer
- and it can modify the value to which the receiver points
- since methods often need to modify their receiver
- pointer receiver are more common than value receivers

```go
package main

import "fmt"

type Rhyme struct {
	name Name
}

type Name struct {
	label string
}

func (c *Rhyme) modify() {
	c.name.label = "Hello"
}

func main() {
	c := Rhyme{
		Name{"Rhyme"},
	}
	c.modify()
	fmt.Println(c.name)
}
```

## methods and pointer indirection

- functions with a `pointer argument`  must take a pointer
- methods with `pointer receiver` take either a value of a pointer

```go
func f(r *Rhyme) {
	fmt.Println(r.name)
}
r := Rhyme{"hello"}
f(r) // compire error
f(&r) // correct
```

```go
func (r *Rhyme) m() {
	fmt.Println(r.name)
}
r.m() // ok
(&r).m() // ok
```

- as a convenience, Go interprets the `r.m()` as `(&r).m()`
- when the method has a pointer receiver


## methods and pointer indirection

- functions that takes a value argument must take a value of that type
- methods with `value receiver` take either a value or a pointer
- as a convenience, the `p.m()` is interpreted as `(*p).m()`

## choosing a value or pointer receiver

- there are two reasons to use a pointer receiver

1. the method can modify the value that its receiver points to 
2. avoid copying the value on each method call.

> in general, all methods on a given type should have either 
> value or pointer receivers, but not a mixture of both.
