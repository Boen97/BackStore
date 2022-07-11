# struct embedding

```go
type Point struct {
  X float64
  Y float64
}
type ColoredPoint struct {
  Point
}
var cp ColoredPoint
cp.X = 1 // without mention Point
```

## methods embedding

```go
var p = ColoredPoint{Point{1,1}}
p.ScaleBy(2) // can call methods of the embedded Point field
```

- the methods of Point have been `promoted` to `ColoredPoint`

- when the compiler resolves a selector such as p.ScaleBy to a method
- it first looks for a directly declared method named ScaleBy
- then for methods promoted once from ColoredPoint's embedded fields
- then for methods promoted twice from embedded fields within Point and RGBA, and so on.

- the compiler reports an error if the selector was ambiguous
- because two methods were promoted from the same rank.

## unnamed struct types to have methods too.

- thanks to embedding, it's possible and sometimes useful for `unnamed` struct types to have methods too.

```go
var cache = struct {
 sync.Mutex
 mapping map[string] string
} {
 mapping: make(map[string]string),
}

func Lookup(key string) string {
 cache.Lock()
 v := cache.mapping[key]
 cache.Unlock()
 return v
}
```