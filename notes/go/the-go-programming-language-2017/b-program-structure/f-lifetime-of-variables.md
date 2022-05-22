# lifetime of variables

- the `lifetime` of a variable is the interval of time during which it exists as the program executes
- the lifetime of a `package-level` variable is the entire execution of the program.
- by contrast, `local-variable` have dynamic lifttimes: 
- a new instance is created each time the declaration statement is executed
- and the variable lives on until it becomes `unreachable`
- functions parameters and results are `local variables` too

- how does the `garbage collector` know that a variable's storage can be reclaimed?
- basic idea is that every package-level variable and every local variable of each currently active function
- can potentially be the start or root of a path to the variable in question
- following pointers and other kinds of references that ultimately lead to the variable
- if no such path exists, the variable has become unreachable

- because the lifetime of a variable is determined only by whether or not it is reachable
- a local variable may outlive a single iteration of the enclosing loop.
- it may continue to exist even after its enclosing function has returned

- a compiler may choose to allocate local variable on the **heap or on the stack**
- but, perhaps suprisingly, this choice is not determined by whether `var` or `new` was used to declare the variable

```go
var global *int
func f() {
    var x int
    x = 1
    global = &x
}
```

- `x` must be `heap-allocate` because it is still reachable from the `global`
- x escapes from f

```go
func g() {
    y := new(int)
    *y = 1
}
```

- when `g` returns, `*y` becomes unreachable and can be recycled.
- it's safe for the compiler to allocate `*y` on the **stack**, even though it was allocated with `new`

- it's a good to keep in mind during performance optimization
- since each variable that escapes requires an extra memory allocation

- Garbage collection is a tremendous help in writing correct programs, but it does not relieve you of the burden of thinking about memory.
- you don't need to explicitly allocate and free memory
- but to write efficient programs you still need to be aware of the lifetime of variables
