# Command-Line Arguments

- most programs process some input to produce some output.
- that's pretty much the definition of computing.
- inputs comes from an external source:
1. a file
2. a network connection
3. the output of another program
4. a user at a keyboard
5. command-line arguments

## the os package

- the os package provides functions and other values for dealing with the operating system in a platform-independent fashion.
- command line arguments are available to a program in a variable named `Args`
- `os.Args`

## os.Args

- os.Args is a slice of strings.
- **Slices** are a fundamental notion in Go.
- for now, think of a slice as a dynamically sized sequence `s` of array elements
- where individual elements can be accessed as `s[i]`
- and `s[m:n]` for a contiguous subsequence
- `len(s)` returns the number of elements
- index start with 0

- the first element `os.Args[0]` is the name of the commmand itself
- the other elements are the arguments that were presented to the program when it started execution

- `s[m:n]` yields a slice that refers to elements m througs n - 1
- `os.Args[1:len(os.Args)]` is the elements we need.
- if m or n is omitted, it defaults to 0 or `len(s)` respectively
- so `os.Args[1:len(os.Args)]` equals `os.Args[1:]`

## implementation of the Unix echo command
> prints its command-line arguments on a single line.

- the order of imports doesn't matter;
- the `gofmt` tool sorts the package names into alphabetical order.

```golang
// Echo1 prints its command-line arguments.
package main

import (
	"fmt"
	"os"
)

func main() {
	var s string
	sep := " "
	for i := 1; i < len(os.Args); i++ {
		s += sep + os.Args[i]
	}
	fmt.Println(s)
}
```

- by conversion, we describe each package in a comment immediately preceding its package declaration
- for a main package, this comment is one or more complete sentences that describe the program as a whole.
- This is a quadratic process that could be costly if the number of arguments is large, but for echo, that’s unlikely.
- `i++` is statement not expression
- so `j = i++` is illegal
- `--i` is illegal as well, because i++ are postfix only

### for loop

- the for loop is the only loop statement in Go.
- it has a number of forms
```
for initialization; condition; post {}
```
- parentheses are never used around the three components of a for loop
- the braces are manadatory
- the opening brace must be on the same line as the post statement.

- `initialization` is optional, and is executed before the loop starts.
- if it is present, it must be a **single statement**, a short declaration, an increment or assignment or function call

- the `condition` is a boolean expression that is evaluated at the beginning of each iteration of the loop
- the `post` statement is executed after the body of the loop

- **any of these components may be omitted**

```
// a traditional while loop
for condition {
}

// a traditional infinite loop
for {

}
```

- another form of the for loop iterates over a range of values from a data type like a string or a slice.

```golang
package main

import (
	"fmt"
	"os"
)

func main() {
	s, sep := "", ""
	for _, arg := range os.Args[1:] {
		s += sep + arg
		sep = " "
	}
	fmt.Println(s)
}
```

- `range` produces a pair of values: the index and the value 
- `_` **blank identifier**

## variable declaration form
1. s := ""
: most compact, used only within a function, not for package-level variables

2. var s string
: rely on default **zero value**

3. var s = ""
: is rarely used except when declaring multiple variables

4. var s string = ""
: explicit about the variable's type

> in practice, you should generally use one of the first two forms
> with explicit initialization to say that the initial value is important 
> and implicit initialization to say that the initial value doesn’t matter.

## a more efficient way

> use `Join` from the `strings` package

```golang
package main

import (
	"fmt"
	"os"
	"strings"
)

func main() {
	fmt.Println(strings.Join(os.Args[1:], " "))
}
```
