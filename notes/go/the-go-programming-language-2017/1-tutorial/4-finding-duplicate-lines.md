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
