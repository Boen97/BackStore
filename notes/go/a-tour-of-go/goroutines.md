# Goroutines

- a `goroutine` is a lightweight thread managed by the Go runtime.
- `go f(x, y, z)` starts a new goroutine running
- the `evaluation` of `f, x, y, z` happens in the `current goroutine`
- the `execution` of `f` happens in the new goroutine.

> Goroutines run in the same address space, so access to shared memory must be synchronized

- the `sync` package provides useful primitives, although you won't need them much in Go as there are other primitives

```go
package main

import (
	"fmt"
	"time"
)

func say(str string) {
	for i := 0; i < 5; i++ {
		time.Sleep(100 * time.Millisecond)
		fmt.Println(str)
	}
}

func main() {
	go say("World")
	say("Hello")
}
```
