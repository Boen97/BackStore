# Switch

- `switch` is a shorter way to write a sequence of `if-else`
- it runs the first case whose value is equal to the condition expression
- Go's only runs the selected case, not all the cases that follow
- Go's switch cases need not be constants, and the values need not be integers.

```go
switch os := runtime.GOOS; os {
    case "linux":
        fmt.Println("linux")
    case "darwin":
        fmt.Println("darwin")
    case "xxx":
        fmt.Println("xxx")
    default:
        fmt.Println("default")
}
```

## switch with no condition

- switch without a condition is the same as `switch true`
- the construct can be a clean way to write long if-then-else chains

```go
t := time.Now()
switch {
case t.Hour() < 12:
    fmt.Println("Good morning")
case t.Hour() < 17:
    fmt.Println("Good afternoon")
default:
    fmt.Println("Good evening")
}
```
