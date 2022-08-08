# Maps

- the zero value of a map is `nil`, a `nil` map has no keys, `nor can keys be added`
- the `make` returns a map of the given type, and ready for use.

```go
var m map[string]int // nil, not ready for use
m := make(map[string]int) // ready for use
```

## Map literals

```go
m2 := map[string]int {
    "Rhyme": 10,
    "Chiang": 20,
}
```

## omit top level type

- if the top-level type is just a type name, you can omit it from the elements of the literals

```go
m3 := map[string]Person {
    "Rhyme": {"Rhyme", 12},
}
```

## mutating maps

```go
m[key] = value // insert
v := m[key] // retrieve
delete(m, key) // delete
e, ok := m[key] // check key
```
