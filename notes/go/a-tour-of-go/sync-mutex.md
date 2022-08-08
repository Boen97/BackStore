# sync.Mutex

## mutual exclusion

- make sure only one goroutine can access a variable at a time to avoid conflicts
- this concept is called `mutual exclusion`
- the conventional name for the data structure that provides it is `mutex`

- Go standard library provides mutual exclusion with `sync.Mutex` and its two methods:

```go
Lock()
UnLock()
```

- we can also use `defer` to ensure the mutex will be unlocked

- the zero value for a `Mutex` is an `unlocked mutex`

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

type SafeCounter struct {
	mu sync.Mutex
	v map[string]int
}

func (c *SafeCounter) Inc(key string) {
	c.mu.Lock()
	c.v[key]++
	c.mu.Unlock()
}

func (c *SafeCounter) Value(key string) int {
	c.mu.Lock()
	defer c.mu.Unlock()
	return c.v[key]
}

func main() {
	c := SafeCounter{v : make(map[string]int)}
	for i := 0; i < 1000; i++ {
		go c.Inc("somekey")
	}
	time.Sleep(time.Second)
	fmt.Println(c.Value("somekey"))
}
```
