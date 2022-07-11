# Method Values and Expressions

## method value
`p.Distance`

- the selector `p.Distance` yields a `method value`
- a function that binds a method to a specific receiver value `p`
- this function can then be invoked without a receiver value
- it needs only the `non-receiver` arguments

```go
type Rocket struct {}
func (r *Rocket) Launch() {}
r := new(Rocket)
time.AfterFunc(10 * time.Second, func() {r.Launch()})
```

- the method value syntax is shorter:
`time.AfterFunc(10 * time.Second, r.Launch)`

> method values are userful when a package's API
> calls for a function value, and the client's desired behaviour
> for that function is to call a method on a specific receiver

## method expression

```go
T.f
(*T).f
```

- T is a type, yields a function value with a regular
- first parameter taking the place of the receiver

```go
type Rocket struct {
	name string
}

func (r *Rocket) Launch() {
	fmt.Println(r.name)
}

func main() {
	r := Rocket {
		name: "Rhyme",
	}
	launch := (*Rocket).Launch
	launch(&r)
}
```

> methods expressions can be helpful when you need a value to 
> represent a choice among several methods belonging to the same
> type so that you can call the chosen method `with many different receivers`

```go
func (p Point) Add(q Point) Point {
	return Point{p.X + q.X, p.Y + q.Y}
}

func (p Point) Sub(q Point) Point {
	return Point{p.X - q.X, p.Y - q.Y}
}

type Path []Point

func (path Path) TranslateBy(offset Point, add bool) {
	var op func(p, q Point) Point
	if add {
		op = Point.Add
	} else {
		op = Point.Sub
	}
	for i := range path {
		path[i] = op(path[i], offset)
	}
}
```
