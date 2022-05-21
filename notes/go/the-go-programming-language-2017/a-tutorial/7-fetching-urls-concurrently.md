# a taste of Go's main concurrency mechanisms, goroutines and channels

> one of the most interesting and novel aspects of Go is its support for **concurrent programming**

- a `goroutine` is a concurrent function execution.
- a `channel` is a communication mechanism that allows one goroutine to pass values of a specified type to another goroutine
- the function `main` runs in a goroutine, and the `go` statement creates additional goroutines

- the `main` function creates a `channel` of strings using `make`
- when one goroutine attempts a send or receive on a channel
- it blocks until another goroutine attempts the corresponding receive or send operation
- at which point the value is transfered and both goroutines proceed.

```golang
package main

import (
	"fmt"
	"io"
	"io/ioutil"
	"net/http"
	"os"
	"time"
)

func main() {
	start := time.Now()
	ch := make(chan string)
	for _, url := range os.Args[1:] {
		go fetch(url, ch)
	}
	for range os.Args[1:] {
		fmt.Println(<-ch)
	}
	fmt.Printf("%.2fs elapsed\n", time.Since(start).Seconds())
}

func fetch(url string, ch chan<- string) {
	start := time.Now()
	resp, err := http.Get(url)
	if err != nil {
		ch <- fmt.Sprint(err)
		return
	}
	nbytes, err := io.Copy(ioutil.Discard, resp.Body)
	resp.Body.Close()
	if err != nil {
		ch <- fmt.Sprintf("while reading %s: %v", url, err)
		return
	}
	secs := time.Since(start).Seconds()
	ch <- fmt.Sprintf("%.2f %7d %s", secs, nbytes, url)
}
```
