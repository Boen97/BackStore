# Packages and Files

- the source code for a package resides in one or more .go files
- usually in a directory whose name ends with the import path.
- for instance, the file of the `gopl.io/ch1/hellworld` package 
- are stored in directory `$GOPATH/src/gopl.io/ch1/hellworld`

- each package serves as a separate `name space` for its declarations

- Packages also let us hide information by controlling which names are visible outside the pack- age, or exported.

## make a package available to the Go community

1. gopl.io/ch2/tempconv/tempconv.go

```go
package tempconv
import "fmt"
type Celsius float64
type Fahrenheit float64
const (
         AbsoluteZeroC Celsius = -273.15
         FreezingC     Celsius = 0
         BoilingC      Celsius = 100
)
func (c Celsius) String() string { return ...}
func (f Fahrenheit) String() string { return fmt.Sprintf("%g°F", f) }
```

2. gopl.io/ch2/tempconv/conv.go

```go
package tempconv
// CToF converts a Celsius temperature to Fahrenheit.
func CToF(c Celsius) Fahrenheit { return Fahrenheit(c*9/5 + 32) }

// FToC converts a Fahrenheit temperature to Celsius.
func FToC(f Fahrenheit) Celsius { return Celsius((f - 32) * 5 / 9) }
```

- when the package is imported, its members are referred to as `tempconv.CToF` and so on.

- the `doc` comment immediately preceding the package declaration documents the package as a whole.
- Only one file in each package should have a package doc comment.
- Extensive doc comments are often placed in a file of their own, conventionally called doc.go.

## imports

- within a Go program, every package is identified by a unique string called its `import path`
- The `import` above lets us refer to names within `gopl.io/ch2/tempconv` by using a `qualified identifier` like `tempconv.CToF`
- by default, the short name is the package name - `tempconv` in this case
- but an `import` declaration may specify an alternative name to avoid a `conflict`

- it is an error to import a package and then not refer to it.
- better still, use the `golang.org/x/tools/cmd/goimports` tool
- which automatically inserts and remove packages from the import declaration as necessary.

## package initialization

- package initialization begins by initializing package-level variables in the order in which they are declared
- except that dependencies are resolved first.
- if the package has multiple `.go` files
- they are initialized in the order in which the files are given to the compiler;
- the `go` tool sorts `.go` files by name before invoking the compiler.
- `func init() {}`
- Such init functions can’t be called or referenced, but otherwise they are normal functions.
- within each file, `init` functions are automatically executed when the program starts
- in the order in which they are declared

- one package is initialized at a time.
- in the order of imports in the program, dependencies first.
- so a package `p` importing `q` can be sure that `q` is fully initialized before `p's` initialization begins.
- initialization proceeds from the bottom up;
- the `main` package is the last to be initialized
