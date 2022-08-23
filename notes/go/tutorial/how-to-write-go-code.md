# How to Write Go Code.

## Code organization

Go programs are organized into packages.
- a package is a collection of source files in the same directory that are `compiled together`
- functions, types, variables, and constants defined in one source file are visible to all other souce files within the same package

a repository contains one or more modules.
a Go repository typically contains only one module.
a file named `go.mod` declares the `module path:` the import path prefix for all packages within the module

each module's path not only serves as an import path prefix for its package, but also indicates where `go` command should look o download it

packages in the standard library do not have a module path prefix.

## first program

```shell
mkdir hello
cd hello
go mod init example/user/hello
```
- hello.go

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, world.")
}
```

- build and install the program

```
$ go install example/user/hello
```

- this command builds the `hello` command, producing an executable binary
- the install directory is controlled by the `GOPATH` and `GOBIN`
  if `GOBIN` is set, binaries are installed to that directory
  if `GOPATH` is set, binaries are installed to the `bin` subdirectory of the first directory in the `GOPATH` list.
  Otherwise, binaries are installed to the `bin` subdirectory of the default `GOPATH`($Home/go)

- `go env -w GOBIN=/somewhere/else/bin`
- `go env -u GOBIN` to unset a variable
