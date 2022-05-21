> Go is a compiled language
> The Go toolchain converts a source program and the things it depends on into instructions in the native machine language of a computer.
- these tools are accessed through a single command called `go` that has a number of subcommands.
- the simplest command is `run`
: which compiles the source code from one or more source files whose names end in .go
: links it with libraries
: then runs the resulting executable file.

> Go natively handles Unicode

## go build helloworld.go

> compile it once and save the compiled result for later use.
> creates an executable binary file called helloworld that can be run any time without further processing.

```shell
$ ./helloworld
```

> go code is organized into packages
> a package consists of one or more .go source files in a single directory that define what package does.

- each source file begins with a package declaration
- here package main, that states which package the file belongs to
- followed by a list of other packages that it imports

- the Go standard library has over 100 packages

## package main and func main

> package main is special
> it defines a standalone executable program, not a library

- `func main` it's where execution of the program begins.

## import declaration

- you must import exactly the packages you need.
- a program will not compile if there are missing imports or if there are unneccessary ones.
- this strict requirement prevents references to unused packages from accumulating as programs evolve.

## semicolons

- Go does not require semicolons at the ends of statements or declarations, except where two or more appear on the same line. 
- **newlines following certain tokens are converted into semicolons**
- so where newlines are placed matters to proper parsing of Go code.
- for example, the opending brace `{` of the function must be on the same line as the end of `func`

## code formatting

- Go takes a strong stance on code formatting
- the `gofmt` tool rewrites code into the standard format
- and the go tool's `fmt` subcommand applies `gofmt` to all the files in the specified package, or the ones in the current directory by default.

- declaring a standard format by fiat eliminates a lot of pointless debate about trivia
- and more importantly, enables a variety of automated source code transformations that would be infeasible if arbitrary formatting were allowed.

## goimports tool
> `goimports` tool additionally manages the insertion and removal of import declarations as needed.
- it is not part of the standard distribution
- but you can obtain it with this command

`$ go get golang.org/x/tools/cmd/goimports`

## go tool
- for most users, the usual way to download and build packages, run their tests, show their documentation, is with the `go` tool.

