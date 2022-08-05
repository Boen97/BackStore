# Methods

- Go does not have classes
- However, you can define methods on types.
- a method is a function with a special receiver argument.

```go
type Rhyme struct {
	name string
}
func (r Rhyme) hello() {
	fmt.Println("Hello", r.name)
}
```
