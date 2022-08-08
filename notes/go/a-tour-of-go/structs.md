## pointers to struct

- get struct field without explicit dereference

```go
p := &s
p.age = 12
(*p).age = 24
```

## struct literals

```go
var (
    v1 = Rhyme{"Rhyme", 12}
    v2 = Rhyme{}
    v3 = Rhyme{name: "Rhyme"}
    p = &Rhyme{}
)
```
