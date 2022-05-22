# The new Function

- another way to create a variable is to use the built-in function `new`
- the expression `new(T)` creates an `unnamed variable` of type `T`
- initializes it to the zero value of `T`
- and returns its address, which is a value of type `*T`

```go
p := new(int) // p, of type *int, points to an unnamed int variable
fmt.Println(*p)
*p = 2
fmt.Println(*p)
```

- a variable created with `new` is no different from an ordinary local variable whose address is taken
- except that there's no need to invent a dummy name
- the `new` is only a syntactic convenience, not a fundamental notion.

- each call to `new` returns a distinct variable with a unique address
```go
p := new(int)
q := new(int)
p == q // false
```
- there is one exception:
- two variables whose type carries no information and is therefore of size zero,
- such as `struct{}` or `[0]int`,
- may, depending on the implementation, have the same address

- the `new` function is relatively rarely used because the most common unnamed variables are of `struct` type.

`func delta(old, new int) int { return new - old }`
-  within delta, the built-in new function is unavailable.
