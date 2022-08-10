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

## Add a test

- ending a file's name with `_test.go` tells the `go test` that this file contains test functions.

```go
package greetings

import "testing"

func TestHello(t *testing.T) {
	name := "Rhyme"
	if name == "rhyme" {
		t.Fatalf(`Need Match Rhyme: current %v`, name)
	}
}
```

- Test function has the form `TestName`
- Where `Name` says something about the specific test

### go test command

- `go test` executest test functions in test files, whose name ends with _test.go
- `go test -v` get verbose output that lists all of the tests and their values.
- the output will include results for only the test that failed.

## compile and install the application

- `go run` command doesn't generate a binary executable
- it is a useful shortcut for compiling and running a program when you're making frequent changes.

- `go build` command compiles the package, along with their dependencies, but it doesn't install the results
- compile the code into an executable
- it will generate a executable file

- `go install` command compiles and intalls the package


3. install the executable so you can run it without specifying its path.

- discover the `Go install path`, where the `go` command will install the current package
- you can discover the install path by running `go list` command

- `$ go list -f '{{.Target}}'`
- it returns `/Users/rhyme/go/bin/hello`
- meaning that binaries are installed to `/Users/rhyme/go/bin`

4. add the Go install directory to your system's shell path.

```shell
export PATH=$PATH:/path/to/your/install/directory
```

- you can change the install target by setting the `GOBIN` variable

```shell
go env -w GOBIN=/path/to/your/bin
```

5. once you've updated the shell path, run the `go install` to compile and install the package
