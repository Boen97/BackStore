# Recover

- if the built-in `recover` function is called within a `deferred function` and the function containing the `defer` is `panicking`
- `recover` ends the current state of panic and returns the `panic value`
- if `recover` is called at any other time, it has not effect and returns `nil`

```go
func Parse(input string) (s *Syntax, err error) {
    defer func() {
        if p := recover(); p != nil {
            err = fmt.Errorf("internal error: %v\n", p)
        }
    }()
    // ...
}
```

> recover only from panics that were intended to be recovered from, which should be rare.
