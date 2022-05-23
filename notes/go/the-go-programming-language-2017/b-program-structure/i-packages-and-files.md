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
