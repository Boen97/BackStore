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
