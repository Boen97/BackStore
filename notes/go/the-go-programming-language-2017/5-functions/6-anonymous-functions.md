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

- the lifetime of a variable is not determined by its scope.

## Caveat: Capturing lteration Variables

- wrong
```go
var rmdirs []func()
for _, dir := range tempDirs() {
    os.MkdirAll(dir, 0755)
    rmdirs = append(rmdirs, func() {
        os.RemoveAll(dir) // incorrect
    })
}
```
> the `for` loop introduces a new lexical block in which the `dir` is declared.
> all function values created by this loop `capture` and `share` the same variable.

- correct 
```go
var rmdirs []func()
for _, d := range tempDirs() {
    dir := d
    os.MkdirAll(dir, 0755)
    rmdirs = append(rmdirs, func() {
        os.RemoveAll(dir)
    })
}
```

- the same problem happens with normal for iteration

```go
var rmdirs []func()
dirs := tempDirs()
for i := 0; i < len(dirs); i++ {
    os.MkdirAll(dirs[i], 0755) // ok
    rmdirs = append(rmdirs, func() {
        os.RemoveAll(dirs[i]) // note : incorrect
    })
}
```

- the problem also happens with `go` and `defer`, which `delay` the execution of a `function value`
