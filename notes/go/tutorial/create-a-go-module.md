# Create a Go module

- in this tutorial you'll create two modules
- the first is a library which is intended to be imported by other libraries or applications.
- the second is a caller application which will use the first.


## go mod edit

- redirect Go tools from its module path to the `local directory`

```shell
go mod edit -replace example.com/greetings=../greetings
```

- `go.mod` 

```go
module example.com/hello

go 1.16

replace example.com/greetings => ../greetings
```

- then run `go mod tidy`

```go
module example.com/hello

go 1.16

replace example.com/greetings => ../greetings

require example.com/greetings v0.0.0-00010101000000-000000000000
```

-  the number following the module path is a `pseudo-version number`

- when reference a published module, the `go.mod` file looks like this

```go
require example.com/greetings v1.1.0
```
