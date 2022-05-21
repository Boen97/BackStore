# a minimal server that returns the path component of the URL

```go
package main

import (
	"fmt"
	"log"
	"net/http"
)

func main() {
	http.HandleFunc("/", handler)
	log.Fatal(http.ListenAndServe("localhost:9999", nil))
}

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Url.Path = %s", r.URL.Path)
}
```

- a request is represented as a struct of type `http.Request`
- which contains a number of related fields, one of which is the URL of the incomming request.

## server2 counts the number of requests

```go
package main

import (
	"fmt"
	"log"
	"net/http"
	"sync"
)

var mu sync.Mutex
var count int

func main() {
	http.HandleFunc("/", handler)
	http.HandleFunc("/count", counter)
	log.Fatal(http.ListenAndServe("localhost:9999", nil))
}

func handler(w http.ResponseWriter, r *http.Request) {
	mu.Lock()
	count++
	mu.Unlock()
	fmt.Fprintf(w, "Url.Path = %s\n", r.URL.Path)
}

func counter(w http.ResponseWriter, r *http.Request) {
	mu.Lock()
	fmt.Fprintf(w, "Count %d\n", count)
	mu.Unlock()
}
```

- the server runs the handler for each incomming request in a separate goroutine
- so that it can serve multiple requests simultaneously.

- however, if two concurrent requests try to update count at the same time, it might be incremented consistently.
- the program would have a serious bug called **race condition**
- to avoid this problem, we must ensure that at most one goroutine access the variable at a time.
- which is the purpose of the `mu.Lock()` and `mu.Unlock()`

## server3 report on the headers and form data

```go
// handler echoes the HTTP request
package main

import (
	"fmt"
	"log"
	"net/http"
)

func main() {
	http.HandleFunc("/", handler)
	log.Fatal(http.ListenAndServe("localhost:9999", nil))
}

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "%s %s %s\n", r.Method, r.URL, r.Proto)
	for k, v := range r.Header  {
		fmt.Fprintf(w, "Header[%q] = %q\n", k, v)
	}
	fmt.Fprintf(w, "Host = %q\n", r.Host)
	fmt.Fprintf(w, "RemoteAddr = %q\n", r.RemoteAddr)
	if err := r.ParseForm(); err != nil {
		log.Print(err)
	}
	for k, v := range r.Form {
		fmt.Fprintf(w, "Form[%q] = %q\n", k, v)
	}
}
```

- `if err := r.ParseForm(); err != nil`
```go
err := r.ParseForm()
if err != nil {
}
```

- go allows a simple statement such as a local variable declaration to precede
- the if condition
- which is particularly useful for error handling
- is shorter and reduces the scope of the variable err
