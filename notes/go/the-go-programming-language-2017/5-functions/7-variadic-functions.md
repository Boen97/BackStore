# Variadic Functions

- to declare a variadic function, the type of the final parameter is preceded by an ellipsis ....

```go
func sum(vals ...int) int {
    total := 0
    for _,val := range vals {
        total += val
    }
    return total
}
```

- implicitly, the caller allocates an array, copies the arguments into it, and passes a slice of the entire array to the function.

## invoke a variadic function when the arguments are already in a slice:
- place an `ellipsis` after the final argument
```go
values := []int{1,2,3}
sum(values...)
```

- the type of a variadic function is distinct from the type of a function with an ordinary slice parameter
```go
func f(...int) {} // func(...int)
func g([]int) {} // func([]int)
```

- the `interface{}` type means that this function can `accept any values` at all for its final arguments
```go
func errorf(linenum int, format string, args ...interface{}) {
	fmt.Fprintf(os.Stderr, "Line %d: ", linenum)
	fmt.Fprintf(os.Stderr, format, args...)
	fmt.Fprintln(os.Stderr)
}
```
