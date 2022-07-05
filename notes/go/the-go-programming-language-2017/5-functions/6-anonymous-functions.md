# Anonymous Functions

- `Named functions` can be declared only at `package level`, but we can use a `function literal` to denote 
- a `function value` within any expression.

- function literals let us define a function call at its point of use.

```go
f := func() int {
    return 123
}
f()
```
