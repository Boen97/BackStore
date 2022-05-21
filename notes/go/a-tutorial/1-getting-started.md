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

## call code in an external package.

1. Visit **pkg.go.dev** and search for a "quote" package.
2. Locate and click the rsc.io/quote package in search results (if you see rsc.io/quote/v3, ignore it for now).
3. In the Documentation section, under Index, note the list of functions you can call from your code. You'll use the Go function.
4. At the top of this page, note that package quote is included in the rsc.io/quote module.

- you can use the **pkg.go.dev** to find published modules whose packages have functions you can use in your own code.
- packages are published in modules -- like `rsc.io/quote` where others can use them.
- modules are imporved with new versions over time.
- and you can upgrade your code to use the imporved versions.

2. in your Go code, import the `rsc.io/quote` package and add a call to its Go function.

```go
package main

import "fmt"
import "rsc.io/quote"

func main() {
	fmt.Println(quote.Go())
}
```

3. Add new module requirements and sums

> Go will add the `quote` module as a requirement, as well as a `go.sum` file for use in authenticating the module.

```
$ go mod tidy
```

4. Run your code.

```shell
$ go run .
Don't communicate by sharing memory, share memory by communicating.
```

