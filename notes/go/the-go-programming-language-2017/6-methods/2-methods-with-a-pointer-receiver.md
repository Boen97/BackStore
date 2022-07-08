# Methods with a Pointer Receiver

- pointer usage

1. modify a variable
2. avoid copy large argument

```go
func (p *Point) ScaleBy(factor float64)  {
  p.X *= factor
  p.Y *= factor
}
```

- the name of this method is `(*Point).ScaleBy`
- the parentheses are necessary, without them, the expression would be parsed as *(Point.ScaleBy).

> convention dictates that if any method of `Point` has a pointer receiver, than all methods of `Point` should have a pointer receiver

- `Names types (Point)` and `pointers to them (*Point)` are the only types that may appear in a receiver declaration.

## names types that are themselves pointer types are not permit on method declaration

```go
type P *int
func (P) f() {} // compile error: invalid receiver type
```

```go
func (*Point) ScaleBy(factor float64) {
  p.X *= factor
  p.Y *= factor
}
r := &Point{1,2}
r.ScaleBy(2)

p := Point{1,2}
pPtr := &p
pPtr.ScaleBy(2)

p := Point{1,2}
(&p).ScaleBy(2)
```

> if the receiver `p` is a variable of type `Point` but the method requires a `*Point` receiver
> we can use this shorthand
`p.ScaleBy(2)`

- the compiler will perform an implicit &p on the variable
- this works only for variables, including struct fields like p.X and array or slice elements like arr[0]

- there's no way to obtain the address of a temporary value.

```go
Point{1,2}.ScaleBy(2) // compile error: can't take address of Point literal
```

## three cases with implicit

- argument: the value passed
- parameter: function parameter

1. receiver argument has the same type as the receiver parameter
2. receiver argument is T and receiver parameter is *T, the compile implicit takes the  address of the variable
3. receiver argument is *T, receiver parameter is T, the compiler implicit dereferences the receiver

> if all the methods of a names type T have a receiver type of T itself(not *T)
> it is safe to copy instances of that type.
> calling any of its methods necessary makes a copy.