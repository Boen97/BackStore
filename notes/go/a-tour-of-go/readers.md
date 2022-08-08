# Reader interface

```go
type Reader interface {
    Read(p []byte) (n int, err error)
}
```

- `io.Reader` represents the read end of a stream of data
- files, network connections, compressors, ciphers
- `io.Reader` returns `io.EOF` error when the stream ends

```go
package main

import (
	"io"
	"os"
	"strings"
)

func main() {
	r := strings.NewReader("Hello, Reader")
	b := make([]byte, 8)
	for {
		_, err := r.Read(b)
		if err == io.EOF {
			break
		}
	}
}
```
