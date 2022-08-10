# Multi-module workspace

- with multi-module workspace, you can tell the Go command
- that you're writing code in multiple modules at the same time
- and easily build and run code in those modules.

> Note: need Go1.18 or later

1. mkdir `workspace`
2. under `workspace`, create `hello` module

## create the workspace

1. in the `workspace`, run

- `$ go work init ./hello`

- the `go work init` command tells go to create a `go.work` file for a workspace containing the modules in the `./hello` directory

- `go.work`
```go
go 1.19

use ./hello
```

### run the program in the workspace directory

`go run jake-ress.com/hello`


## Add another module

`go work use ./another`

- this will allow us to use the new code in the same workspace
- instead of the version of the module in the module cache that are download with the `go get`

- `go.work` can be used instead of adding `replace` directives to work across multiple modules.
- since the two modules are in the same workspace, it is easy to make a change in one module and use it in another

## other commands

- `go work edit` edits the go.work file similarly to `go mod edit`
- `go work sync` syncs dependencies from the workspace's build list into each of the workspace module
