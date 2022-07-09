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