# Errors

- the `error` interface

```go
type error interface {
    Error() string
}
```

- as with `fmt.Stringer`, the `fmt` package looks for the `error` interface when printing values

```go
package main

import (
	"fmt"
	"time"
)

type MyError struct {
	when time.Time
	what string
}

func (e *MyError) Error() string {
	return fmt.Sprintf("at %v, %s", e.when, e.what)
}

func run() error {
	return &MyError{
		time.Now(),
		"It errors",
	}
}

func main() {
	if err := run(); err != nil {
		fmt.Println(err)
	}
}
```
