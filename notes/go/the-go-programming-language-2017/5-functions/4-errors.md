- success is not assured because it depends on factors beyond the programmer's control.
- any function that does `I/O`, must confront the possibility of error.

> failure is just one of several expected behaviors.

> Go's `error` are `ordinary values`, not `exceptions`

## Go's error design
- `exceptions` tend to entangle the `description of an error` with `the control flow required` to handle it.
- often leading to an undesirable outcome.
- `routine errors` are reported to the end user in the form of an `incomprehensible stack trace`,
- full of information about the `structure of the program` but leaking `intelligible context about what went wrong`

> by contrast, Go use ordinary control-flow like `if` and `return` to response to errors.
> This style undeniably demands that more attention be paid to `error-handling-logic`, which is `most important`

## error-handling strategies

> when a function call returns an error, it's the `caller's responsibility` to check it and take appropriate action.

### 1. propagate error
> first and most common, is to `propagate` the error, so that a failure in a `subroutine` becomes a failure of the `calling routine`

- when the error is ultimately handled by the program's `main` function
- it should provide a clear causal `chain` from the `root problem` to the `overall failure`
- reminiscent of a `NASA` accident investigation:
: `genesis: crashed: no parachute: G-switch failed: bad relay orientation`

- because error messages are frequently chained together, message strings should not be `capitalized` and `newlines` should be avoided.
- the resulting errors may be long, but they will be `self-contained` when found by tools like `grep`

- when designing error messages, be deliberate, so that each one is a meaningful description of the problem 
- with sufficient and relevant detail
- and be `consistent`, so that errors returned by the same function or by a group of functions in the same package
- are similar in form and can be dealt with in the same way.

- for example, the `os` package guarantees that every error returned by a file operation,
- such as `os.Open` or the `Read, Write` or `Close` methods of an open file
- decribes not just the `nature of the failure`(permission denied, no such directory)
- but also `the name of the file`, so the caller needn't include this information in the error messages it constructs

- in general, the call `f(x)` is responsible for reporting the `attempted operation f` 
- and the argument value `x` as they relate to the context of the `error`
- the `caller` is responsible for adding further information that it has but the call `f(x)` does not.

### 2. second strategy for handling errors
> for errors that represent transient or unpredictable problems, it may make sense to `retry` the failed operation.
> possibly with a delay between tries and with a `limit on the number of attempts` or the `time` spent trying before giving up entirely

```go
package main

import (
	"fmt"
	"log"
	"net/http"
	"time"
)

func main() {
	err := waitForServer("")
	if err != nil {
		fmt.Println(err)
	}
}

func waitForServer(url string) error {
	const timeout = 1 * time.Minute
	deadline := time.Now().Add(timeout)
	for tries := 0; time.Now().Before(deadline); tries++ {
		_, err := http.Head(url)
		if err == nil {
			return nil
		}
		log.Printf("server not responding (%s); retrying...", err)
		time.Sleep(time.Second << uint(tries))
	}
	return fmt.Errorf("server %s failed to respond after %s", url, timeout)
}
```

### 3. stop the program gracefully

- if progress is impossible, the caller can print the error and `stop the program gracefully`.
- but this course of action should generally be reserved for the `main package` of a program.
- `library functions` should usually propagate errors to the caller
- unless the error is a sign of an `internal inconsistency-that is, a bug`

```go
// (in function main)
if err := waitForServer(url); err != nil {
    fmt.Fprintf(os.Stderr, "Site is down: %v\n", err)
    os.Exit(1)
}

if err := waitForServer(url); err != nil {
    log.Fatalf("Site is down: %v\n", err)
}
```

- all the `log` functions, by default, prefixes the `time` and `date` to the error message.

### 4. log the error and then continue.

### 5. safely ignore an error entirely

## Go's error handling rhythm.

- after checking an error, `failure` is usually dealt with `before success`.
- if failure causes the function to return, the logic for success is not indented within an `else` block
