# Defer

- a defer statement defers the execution of a function until the surrounding functions returns.
- the deferred call's arguments are evaluated immediately,
- but the function call is not executed until the surrounding function returns

```go
defer fmt.Println("World")
fmt.Println("Hello")
```

- expression in defer must be `function call`

## Stacking defers

- deffered function calls are pushed onto a stack
- when a functon returns, its deferred calls are executed in last-in-first-out order.

```go
for i := 0; i <= 10; i++ {
    defer fmt.Println(i)
}
fmt.Println("start counting")
```
