# Function Declarations

```go
func hypot(x, y float64) float64 {
    return math.Sqrt(x*x + y*y)
}
hypot(3, 4)
```

- `x and y` are `parameters` in the declaration
- `3 and 4` are `arguments` of the call

- a function that has a result list must end with a `return` statement
- unless execution clearly cannot reach the end of the function, such as `panic` or a `infinite for loop with no break`

## parameters of the same type can be factored

```go
func hello(a,b,c int) int {}
```

## four way to declear a function with two parameters and one result

```go
func add(x int, y int) int { return x + y }
func sub(x, y int)(z int) { z = x - y; return }
func first(x int, _ int) int { return x }
func zero(int, int) int { return 0 }

fmt.Printf("%T\n", add)  // func(int, int) int
```

- the type of a function is called its `signature`
- two functions have the `same type or signature` if they have the same sequence of `parameter types` and the same sequence of `result types`

- go has no concept of `default parameter values`, nor any way to specify `arguments by name`

## Arguments are passed by `value`

- arguments are passed by `value`, so the function receives a copy of each argument

## function declaration without a body

- a function declaration without a body, indicating that the function is implemented in a language other than Go.

```go
package math

func Sin(x float64) float64 // implemented in assembly language
```
