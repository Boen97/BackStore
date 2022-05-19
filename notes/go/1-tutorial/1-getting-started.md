# Get started with Go

## enable dependency tracking for your code.
- when your code imports packages contained in other modules, you manage those dependencies through your code's own module.
- that module is defined by a `go.mod` file that tracks the modules that provides those packages.
- that `go.mod` file stays with your code. including in your source code repository.

### createing a `go.mod` file
- to enable dependency tracking for your code by creating a go.mod file
- run the `go mod init` comand
- giving it the name of the module your code will be in.
- the name is the module's **module path**.

> $ go mod init example/hello

- in actual development, the module path will typically be the repository location where your source code will be kept.
- for example, the module path might be `github.com/mymoudle`
- if you plan to publish your module for others to use.
- the module path must be a location from with Go tools can download your module.

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello World")
}
```

- declare a `main` package (a package is a way to group functions, and it's made up all the files in the same directory)
- import the `fmt` package, and is one of the `standard library` packages you got when you install Go.

### run you code

- `go run .`
- `go help`
