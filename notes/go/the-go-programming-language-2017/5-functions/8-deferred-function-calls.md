# Deferred Function Calls

## title1

```go
package main

import (
	"fmt"
	"net/http"
	"strings"

	"golang.org/x/net/html"
)

func forEachNode(n *html.Node, pre, post func(n *html.Node)) {
	if pre != nil {
		pre(n)
	}
	for c := n.FirstChild; c != nil; c = c.NextSibling {
		forEachNode(c, pre, post)
	}
	if post != nil {
		post(n)
	}
}

func title(url string) error {
	resp, err := http.Get(url)
	if err != nil {
		return err
	}
	ct := resp.Header.Get("Content-Type")
	if ct != "text/html" && !strings.HasPrefix(ct, "text/html;") {
		resp.Body.Close()
		return fmt.Errorf("%s has type %s, not text/html", url, ct)
	}
	doc, err := html.Parse(resp.Body)
	resp.Body.Close()
	if err != nil {
		return fmt.Errorf("parsing %s as HTML: %v", url, err)
	}
	visitNode := func(n *html.Node) {
		if n.Type == html.ElementNode && n.Data == "title" && n.FirstChild != nil {
			fmt.Println(n.FirstChild.Data)
		}
	}
	forEachNode(doc, visitNode, nil)
	return nil
}

func main() {
	url := "https://google.com"
	err := title(url)
	if (err != nil) {
		fmt.Printf("get url %s err %v", url, err)
	}
}
```

- `resp.Body.Close()` are duplicate code, as functions grow more complex and have to handle more errors,
- such duplication of `clean-up` logic may become a maintenance problem.

- Go's `defer` makes things simpler.

## `defer` keyword

> the function and argument expressions are evaluated when the statement is executed.
> but the actual call is `deferred` until the function that contains the `defer` statement has finished.
> whether normally, by executing a return statement or falling off the end, or abnormally, by panicking.

- any number of calls may be deferred, they are executed in the reverse of the order in which they were deferred.

> a `defer` statement is often used with paired operations like open and close, connect and disconnect, or lock and unlock
> to ensure that resources are released in all cases, no matter how complex the control flow.

> the right place for a `defer` statement that releases a resource is immediately after the resource has been successfully acquired.

```go
resp, err := http.Get(url)
if err != nil {
    return err
}
defer resp.Body.Close()
```

```go
mu.Lock()
defer mu.Unlock()
```

### the defer statement can also be used to pair "on entry" and 'on exit' actions when debugging a complex function.
```go
func bigSlowOperation() {
    defer trace('bigSlowOperation')() // don't forget the ()
    // lots of work
}
func trace(msg string) func() {
    start := time.Now()
    log.Printf("enter %s", msg)
    return func() {
        log.Printf("exit %s (%s)", msg, time.Since(start))
    }
}
```

### a `deferred` anonymous function can observe the functions' results

```go
func double(x int) (result int) {
	defer func() {fmt.Printf("double(%d) = %d\n", x, result)}()
	return x + x
}
```

### a `deferred` anonymous function can even change the values that the enclosing function returns to its caller

```go
func triple(x int) (result int) {
    defer func() {result += x}()
    return x + x
}
triple(4) // 12
```

### a `defer` statement in a loop

- the code below could run out of file descriptions

```go
for _, filename := range filenames {
    f, err := os.Open(filename)
    if err != nil {
        return err
    }
    defer f.Close() // Note risky; could run out of file descriptors.
}
```

> solution1, wrap into a function
```go
for _, filename := range filenames {
   if err := doFile(filename); err != nil {
       return err
   }
}
func doFile(filename string) error {
    f, err := os.Open(filename)
    if err != nil {
        return err
    }
    defer f.Close()
}
```

- On many file systems, notably NFS, write errors are not reported immediately but may be postponed until the file is closed.
- Fail- ure to check the result of the close operation could cause serious data loss to go unnoticed.
- It’s tempting to use a second deferred call, to f.Close, to close the local file, but this would be subtly wrong because os.Create opens a file for writing, creating it as needed.
```go
n, err = io.Copy(f, resp.Body)
// Close file, but prefer error from Copy, if any.
if closeErr := f.Close(); err == nil {
    err = closeErr
}
```
