# A Simple Sqrt Implementation

```go
package main

import (
	"fmt"
	"math"
)

func Sqrt(x float64) float64 {
	z := 1.0
	for oldZ := 0.0; math.Abs(oldZ-z) > 1e-6; {
		oldZ = z
		z -= (z*z - x) / (2 * z)
		fmt.Println(z)
	}
	return z
}

func main() {
	fmt.Println(Sqrt(4))
}
```
