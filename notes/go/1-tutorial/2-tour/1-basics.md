## packages

- every Go program is made up of packages
- program start running in package `main`

```golang
package main

import (
	"fmt"
	"rsc.io/quote/v4"
)

func main() {
	fmt.Println(quote.Go())
}
```

- the package name is the same as the last element of the import path.

## import
1. factored import statement
```golang
import (
    "fmt"
    "math"
)
```
2. multiple import statement
```golang
import fmt
import math
```

## exported names
