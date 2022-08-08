# Pointers

- a pointer holds the memory address of a value.
- the type `*T` is a pointer to a `T` value, its zero value is `nil`

```go
var p *int
```

- the `&` operator generates a pointer to its operand.

```go
i := 42
p = &i
```

- the `*` operator denotes the pointer's underlying value.

```go
fmt.Println(*p)
*p = 21
```

- this is known as `dereferencing` or `indirecting`
