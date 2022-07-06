# Panic

- when the Go `runtime` detects these mistakes, it `panics`
- during a typical panic, normal execution stops, all `deferred function calls` in that `goroutine` are executed.
- and the program `crashes` with a log message

- the `log message` includes the `panic value`, which is usually an error message of some sort, and for `each goroutine`, a `stack trace`
- showing the stack of function calls that were active at the time of the panic.

- the log message often has enough information to diagnose the problem.
- so it should be included in a bug report about a panicking program.

## call `panic` function directly

- not all panics come from the runtime, the built-in `panic` function may be called directly

- a panic is often the `best` thing to do when some `impossible situation` happens.
```go
switch s {
case 1:
case 2:
default:
    panic("error")
}
```

## there is no point asserting a condition that the runtime will check for you.
```go
func test(s *Buffer) {
    if s == nil {
        panic("s is nil") // unnecessary
    }
}
```

## panic vs exceptions in other language

- since a panic causes the program to crash, it is generally used for grave errors.
- in a robust program, `expected errors` should be handled gracefully, and they are best dealt with `error` values.

- example, consider the `regexp.Compile`, which compiles a regular expression into an efficient form for matching
- it returns an error if called with an ill-formed pattern.
- checking this error is unnecessary and burdensome `if the caller knows that` a particular call `cannot fail`
- in such cases, it's reasonable for the caller to handle an error by `panicking`, since it is belived to be impossible

## defferd functions when panic happen

- when a panic happen, all deferred functions are run in `reverse order`, starting with those of the `topmost` function 
- on the stack and proceeding up to `main`

```go
package main

import "fmt"

func f(x int) {
	fmt.Printf("f(%d)\n", x+0/x) // panic if x = 0
	defer fmt.Printf("defer %d\n", x)
	f(x - 1)
}
func main() {
	f(3)
}
```
- output
```
f(3)
f(2)
f(1)
defer(1)
defer(2)
defer(3)
```

## dump the stack 

- the `runtime` package lets the programmer dump the stack
```go
func main() {
   defer printStack() 
   f(3)
}
func printStack() {
    var buf [4096]byte
    n := runtime.Stack(buf[:], false)
    os.Stdout.Write(buf[:n])
}
```
