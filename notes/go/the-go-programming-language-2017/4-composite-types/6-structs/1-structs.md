# Structs

> a struct is an aggregate data type that groups together zero or more named values of arbitrary types as a single entity.

- each value is called a `field`

```go
type Empolyee struct {
    ID int
    Name string
    Address string
    DoB time.Time
    Position string
    Salary int
}
```

- a named struct type `S` can't declare a field of the same type `S`: an aggregate value cannot contain itself.
- but `S` may declare a field of the `pointer` type `*S`, which let us create recursive data structures like `linked list` and `trees`

## empty struct

- the struct type with no fields is called the `empty struct`, written `struct{}`

## struct literal

```go
type Point struct{X, Y int}
p := Point{1,2}
```

- named fields

```go
anim := gif.GIF{LoopCount: nframes}
```

- the named and unnamed forms cannot be mixed in the same literal.

## struct values as arguments

- for efficiency, larger struct types are usually passed to or return from functions indirectly using a `pointer`

```go
func Bonus(e *Employee, percent int) int {
}
```

## shorthand notation of struct

- use this shorthand notation to create and initialize a `struct` variable and obtain its address:

```go
pp := &Point{1,2}
// it is exaclty equivalent to
pp := new(Point)
*pp = Point(1,2)
```

## comparing structs

- if all the fields of a struct are comparable, the struct itself is comparable.
```go
type Point struct{X, Y int}
p := Point(1,2)
q := Point(2,1)
q == q // false
```

- comparable struct types, like other comparable types, can be used as the key type of  a map.

```go
package main

func main() {
	type Address struct{
		hostname string
		port int
	}
	hits := make(map[Address]int)
	hits[Address{"golang.org", 443}]++
}
```

## Struct Embedding and Anonymous Fields

- Go's unusual `struct embedding` mechanism 
- let us use one named struct type as an `anonymous field` field of another struct type
- providing a convenient syntactic shortcut so that a simple dot expression like `x.f` can stand for a chain of fields like `x.d.e.f`

```go
type Point struct {
    X, Y int
}
type Circle struct {
    Center Point
    Radius int
}
type Wheel struct {
    Circle Circle
    Spokes int
}
```

- this makes accessing the fields of a Wheel more `verbose`

```go
var w Wheel
w.Circle.Center.X = 8
```

- Go lets us declare a field `with a type but no name`, such fields are called `anonymous fields`
- the type of the field must be a `named type` or a pointer to a `named type`

- above, a `Point` is `embedded` within `Circle`, `Circle` is `embedded` within `Wheel`

```go
var w Wheel
w.X = 8 // equivalent to w.Circle.Point.X = 8
```
- there's no corresponding shorthand for the struct literal syntax.

`fmt.Printf("%#v\n", w)`
- the `#` adverb causes `%v` verb to display values in a form similar to Go's syntax

- because `anonymous` fields do have implicit names, you can't have two `anonymous` fields of the same type since their names would conflict

> `anonymous field` need not be struct types
> any named type or pointer to a named type will do.

- the outer struct type gains not just the fields of the embedded type but its methods too.
- this mechanism is the main way that complex object behaviors are composed from simpler ones.
- `Composition` is central to `object-oriented` programming in Go.
