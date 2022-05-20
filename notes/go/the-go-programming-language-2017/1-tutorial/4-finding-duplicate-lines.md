# Finding Duplicate Lines

> programs for file copying, printing, searching, sorting, counting, and like all have a similar structure:
> a loop over the input, some computation on each element, and generation of output on the fly or at the end.

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	counts := make(map[string]int)
	input := bufio.NewScanner(os.Stdin)
	for input.Scan() {
		counts[input.Text()]++
	}
	for line, n := range counts {
		if n > 1 {
			fmt.Println("%d\t%s\n", n, line)
		}
	}
}
```

- a `map` holds a set of key/value pairs and provides constant-time operations to store, retrieve, or test for an item in the set.
- the key may be of any type whose values can be compared with `==`, strings being the most common example.
- the value may be of any type at all.
- the build-in function `make` creates a new empty map
- the order of `map` iteration is not specified, but in practice it is random, varing from one run to another.
- the design is intentional, since it prevents programs from relying on any particular ordering where none is guaranteed.
- `bufio` package helps make input and putput efficient and convenient.
- one of its most useful features is a type called `Scanner` that reads input and breaks it into lines or words.

`input := bufio.NewScanner(os.Stdin)`
- the scanner reads from the program's standard input
- each call to `input.Scan()` reads the next line and removes the newline character from the end.
- the result can be retrieved by `input.Text()`
- the `Scan` function returns true if there is a line and false when there is no more input

- the function `fmt.Printf`, like `printf` in C, produces formatted output from a list of expressions.
- `%d` formates an integer operand using decimal notation
- `%s` expands to the value of a string operand
- `Printf` has over a dozen such conversions, which Go call `verbs`
- `%x, %o, %b` integer in hexadecimal, octal, binary
- `%f, %g, %e` floating-poine number: 3.141593, 3.141592653589793, 3.141593e+00 (e+ 是 简写， 等同于 10^0 次)
- `%t` boolean: true or false
- `%c` rune (Unicode code point)
- `%s` string
- `%q` quoted string "abc" or rune 'c'
- `%v` any value in a natural format
- `%T` type of any value.
- `%%` literal percent sign (no operand)

- the format string also contains a tab `\t` and a newline `\n`
- String literal may contain such `escape sequences` for representing otherwise invisible characters
- `Printf` does not write a newline by default.
- by convention, formatting functions whose names end in `f`
- such as `log.Printf` and `fmt.Errorf`, use the formatting rules of `fmt.Printf`
- those names end in `ln` follow `Println`

## dup2 reads from stdin or from a list of named files.

- function `os.Open` returns two values
- the first is an open file (`*os.File`) that is used in subsequence reads by the Scanner
- the second result of `os.Open` is a value of the built-in error type.
- if `err` equals the special build-in value `nil`, the file was opened successfully
- the file is read, and when the end of the input is reached, `Close` closes the file and releases any resource.
- if `err` is not nil, something went wrong
- in that case, the err value describes the problem.
- `Fprintf` prints a message on the standard error stream 

- the call to `countLines` precedes its declaration.
- `Functions` and other package-level entities may be declared in any order.

- when a map is passed to a function, the function receives a copy of the reference
- so any changes the called function makes to the underlying data structure
- will be visible through the caller's map reference too.

- the versions of `dup` operate in a `streaming` mode in which input is read and broken into lines as needed
- so in principle these programs can handle an arbitrary amount of input.
- an alternative approach is to read the entire input into memory in one big gulp
- split it into lines all at once, then process the lines.

```golang
// Dup2 prints the
// ....
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	counts := make(map[string]int)
	files := os.Args[1:]
	if len(files) == 0 {
		countLines(os.Stdin, counts)
	} else {
		for _, arg := range files {
			f, err := os.Open(arg)
			if err != nil {
				fmt.Fprintf(os.Stderr, "dup2: %v\n", err)
				continue
			}
			countLines(f, counts)
			f.Close()
		}
	}
}

func countLines(f *os.File, counts map[string]int) {
	input := bufio.NewScanner(f)
	for input.Scan() {
		counts[input.Text()]++
	}
}
```

## dup3 read entire input into memory

```golang
package main

import (
	"fmt"
	"io/ioutil"
	"os"
	"strings"
)

func main() {
	counts := make(map[string]int)
	for _, filename := range os.Args[1:] {
		data, err := ioutil.ReadFile(filename)
		if err != nil {
			fmt.Fprintf(os.Stderr, "dup3 %v\n", err)
			continue
		}
		for _, line := range strings.Split(string(data), "\n") {
			counts[line]++
		}
	}
	for line, n := range counts {
		if n > 1 {
			fmt.Printf("%d\t%s\n", n, line)
		}
	}
}
```

> in Go, interfaces are implemented implicitly, like **Duck Typing**
