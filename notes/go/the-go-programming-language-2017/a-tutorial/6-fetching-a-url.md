# Fetching a URL

> Go provides a collection of packages, grouped under `net`
> that make it easy to send and receive information through the Internet
> make low-level network connections, and set up servers
> for which Go's concurrency features are particularly useful.

```golang
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"os"
)

func main() {
	for _, url := range os.Args[1:] {
		resp, err := http.Get(url)
		if err != nil {
			fmt.Fprintf(os.Stderr, "fetch: %v\n", err)
			os.Exit(1)
		}
		b, err := ioutil.ReadAll(resp.Body)
		resp.Body.Close()
		if err != nil {
			fmt.Fprintf(os.Stderr, "fetch reading %s: %v\n", url, err)
			os.Exit(1)
		}
		fmt.Printf("%s", b)
	}
}
```

- the `http.Get` makes an HTTP request and if there is no error, returns the result in the response struct `resp`
- the `Body` field of `resp` contains the server response as a readable stream.
- `ioutil.ReadAll` reads the entire response
- the `Body` stream is closed to avoid leaking resources
- `os.Exit(1)` causes the process to exit with a status code of 1.

```golang
package main

import (
	"fmt"
	"io"
	"net/http"
	"os"
	"strings"
)

func main() {
	for _, url := range os.Args[1:] {
		newUrl := url
		const prefix = "http://"
		if !strings.HasPrefix(url, prefix) {
			newUrl = prefix + url
		}
		resp, err := http.Get(newUrl)
		if err != nil {
			fmt.Fprintf(os.Stderr, "fetch: %v\n", err)
			os.Exit(1)
		}
		fmt.Printf("%s\n", resp.Status)
		written, err := io.Copy(os.Stdout, resp.Body)
		resp.Body.Close()
		if err != nil {
			fmt.Fprintf(os.Stderr, "fetch: %v\n", err)
			os.Exit(1)
		}
		fmt.Printf("written: %d\n", written)
	}
}
```
