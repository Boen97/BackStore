# Recursion

- `recursion` is a powerful technique for many problems, and of course it's essential for processing `recursive data structures`

- `golang.org/x/net/html` is a non-standard package, which provides an `HTML` parser
- the `golang.org/x/...` repositories hold packages designed and maintained by the `Go team`
- these packages are not in the standard library because they're still under development or 
- because they're rarely needed by the Go programmers.

- `html.Parse` function reads a sequence of bytes, parses them, and returns the `root of the HTML document tree`, which is an `html.Node`

## Go implementations of `variable-size` stacks

- Go use `variable-size` stacks that start small
- and grow as needed up to a limit on the order of a gigabyte.
- this let us use recursion `safely` and `without worrying about overflow`

```go
package main

import (
	"fmt"
	"os"

	"golang.org/x/net/html"
)

func main() {
	doc, err := html.Parse(os.Stdin)
	if err != nil {
		fmt.Fprintf(os.Stderr, "findlinks: %v\n", err)
		os.Exit(1)
	}
	for _, link := range visit(nil, doc) {
		fmt.Println(link)
	}
}

func visit(links []string, n *html.Node) []string {
	if n.Type == html.ElementNode && n.Data == "a" {
		for _, a := range n.Attr {
			if a.Key == "href" {
				links = append(links, a.Val)
			}
		}
	}
	for c := n.FirstChild; c != nil; c = c.NextSibling {
		links = visit(links, c)
	}
	return links
}
```
