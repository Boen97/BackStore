# Function Values

> functions are `first-class` values in Go: like other `values`, `function values` have `types`
> and they may be assigned to variables or passed to or returned from functions

- the zero value of a function is `nil`
- function values may be compared with `nil`
- but function are `not comparable`, so they may not be compared against each other or used as keys in a map.

- `function values` let us parameterize our functions over not just data, but `behavior too`
- for example, `strings.Map` applies a function to each character
```go
func add1(r rune) rune { return r + 1 }
strings.Map(add1, 'Hello')
```
