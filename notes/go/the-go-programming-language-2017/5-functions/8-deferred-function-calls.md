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
