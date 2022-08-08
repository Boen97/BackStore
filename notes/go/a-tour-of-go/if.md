# If

- `if` like `for`, can emit the `parentheses`, but `braces` are required

## If with a short statement

- like `for`, `if` can start with a short statement to execute `before the condition`

```go
if y := 200; y > 100 {
    fmt.Println("y > 100")
}
```

## If and else

> variables declared inside an `if` short statement are also available inside any of the `else` blocks

```go
if a := 0; a > 100 {
    fmt.Println("a > 100", a)
} else if a == 0 {
    fmt.Println("a === 0", a)
} else {
    fmt.Println("a < 100", a)
}
```
