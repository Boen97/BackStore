# Channels

> channels are a `typed conduit` through which you can send and receive values with the channel operator, `<-`

```go
ch <- v // send v to channel ch.
v := <-ch // receive from ch, and assign value to v
```

- the data flows in the direction of the arrow.

- like maps and slices, channels must be created before use:

`ch := make(chan int)`

- by default, sends and receives `block` until the other side is ready.
- this allows goroutines to `synchronize` without explicit locks or condition variables

```go
package main

import "fmt"

func sum(s []int, c chan int) {
	sum := 0
	for _, v := range s {
		sum += v
	}
	c <- sum
}

func main() {
	s := []int {1,2,3,4,5,6}
	c := make(chan int)
	go sum(s[:len(s) / 2], c)
	go sum(s[len(s) / 2:], c)
	x, y := <-c, <-c
	fmt.Println(x, y, x + y)
}
```

## Buffered Channels

- channels can be buffered

> sends to a buffered channel `block only when the buffer is full`
> receives block when the buffer is empty

```go
package main

import "fmt"

func main() {
	ch := make(chan int, 2)
	ch <- 1
	ch <- 2
	fmt.Println(<-ch, <-ch)
}
```
