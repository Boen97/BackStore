# Type Assertions

- type assertion provides access to an interface value's underlying concrete value

```go
var i interface{} = "Rhyme"
s, ok := i.(string)
fmt.Printf("%T, %v, %v", s, s, ok)
```
