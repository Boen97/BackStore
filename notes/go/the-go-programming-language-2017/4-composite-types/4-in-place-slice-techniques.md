# In-Place Slice Techniques

```go
func nonempty(strings []string) []string {
	i := 0
	for _, s := range strings {
		if s != "" {
			strings[i] = s
			i++
		}
	}
	return strings[:i]
}
```

- the underlying array is `modified` during the `nonempty` function call
- the subtle part is the input slice and output slice `share the same underlying array`

## a slice can be used to implement a stack

```go
stack = append(stack, v)
```

- the top of the stack

```go
top := stack[len(stack) - 1]
```

- pop

```go
stack = stack[:len(stack) - 1]
```

- remove an element from the middle of a slice, and preserve the order
```go
func remove(slice []int, i int) []int {
    copy(slice[i:], slice[i+1:])
    return slice[:len(slice) - 1]
}
```

- if we don't need to preserve the order, we can just move the last element into the gap
```go
func remove(slice []int, i int) []int {
    slice[i] = slice[len(slice) - 1]
    return slice[:len(slice) - 1]
}
```
