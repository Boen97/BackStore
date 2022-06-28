# Mutiple Return Values

- a function can return more than one result.

```go
package main

import (
	"fmt"
	"net/http"
	"os"
	"golang.org/x/net/html"
)

func main() {
	for _, url := range os.Args[1:] {
		links, err := findLinks(url)
		if err != nil {
			fmt.Fprintf(os.Stderr, "findlinks: %v\n", err)
			continue
		}
		for _, link := range links {
			fmt.Println(link)
		}
	}
}

func findLinks(url string) ([]string, error) {
	resp, err := http.Get(url)
	if err != nil {
		return nil, err
	}
	if resp.StatusCode != http.StatusOK {
		resp.Body.Close()
		return nil, fmt.Errorf("getting %s: %s", url, resp.Status)
	}
	doc, err := html.Parse(resp.Body)
	resp.Body.Close()
	if err != nil {
		return nil, fmt.Errorf("parsing %s as HTML: %v", url, err)
	}
	return visit(nil, doc), nil
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

- multiple values returned from functions

```go
func findLinksLog(url string) ([]string, error) {
  findLinks(url)
}
```

```go
fmt.Println(findLinks(url))

links, err := findLinks(url)
log.Println(links, err)
```

- names with multiple return values

```go
func Size() (width, height int)
```
- in convention, a final `bool`m result indicates success, an `error` result often needs no explanation.

## bare return 

- in a function with named results, the operands of a `return` statement may be omitted.

```go
func hello() (name string, age int) {
	name = "Rhyme"
	age = 123
	return
}
```
