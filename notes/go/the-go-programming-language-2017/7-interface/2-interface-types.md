# Interface Types

- an interface type specifies a set of methods that a concrete type must possess
- to be considered an instance of that interface

## naming convention for many of Go's single-method interfaces

```go

type Reader interface {
    Read(p []byte) (n int, err error)
}
type Closer interface {
    Close() error
}
type ReadWriter interface {
    Reader
    Writer
}
type ReadWriteCloser interface {
    Reader
    Writer
    Closer
}
type ReadWriter interface {
    Read(p []byte) (n int, err error)
    Writer
}
```
