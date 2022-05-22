# Pointers

> a pointer value is the address of a variable
> a pointer is thus the location at which a value is stored.
> not every value has an address, but every variable does.
> with a pointer, we can read or update the value of a variable indirectly
> without using or even knowing the name of the variable, if indeed it has a name.

- if a variable is declared `var x int`, the expression `&x` (address of x)*  yields a pointer to an integer variable
- that is, a value of type `*int`, which is pronounced **pointer to int**
- if this value is called `p`, we say **p points to x**, or **p contains the address of x**
- the variable to which p points is written `*p`, which yields the value of that variable, an int
- when `*p` on the left-hand side of an assignment, it updates the variable

```go
x := 1
p := &x // p, of type `*int` points to x
fmt.Println(*p) // "1"
*p = 2
fmt.Println(x) // 2
```

- each component of a variable of aggregate type - a field of a struct or an element of an array
- is also a variable and thus has an address too.

- variables are sometimes described as **addressable values**

- the zero value for a pointer of any type is `nil`
- pointers are comparable
- two pointers are equal if and only if they point to the same variable or both are nil

```go
var x, y int
&x == &x // true
&x == &y // false
&x == nil // false
```

- it is perfectly safe for a function to return the address of a local variable

```go
var p = f()
fun f() *int {
    v := 1
    return &v
}
f() == f() // false
```

- the local v will remain in existence even after the call has returned

- because a pointer contains the address of a variable, passing a pointer argument to a function
- makes it possible for the function to update the variable that was indirectly passed.

```go
func incr(p *int) int {
	*p++
	return *p
}
```

- each time we take the address of a variable or copy a pointer
- we create **new alias** or ways to identify the same variable
- for example, `*p` is an alias for `v`
- **pointer alias** is useful because it allow us to access a variable without using its name
- but this is a double-edged sword:
- to find all the statements that access a variable, we have to know all its alias.

- it's not just pointers that create aliases
- aliasing also occurs when we copy values of other reference types like slice, maps, and channels
- and even structs, and interfaces that contain these types.

## flag package

> pointers are key to the **flag package**, which uses a program's command-line arguments
> to set the values of certain variables distributed throughout the program.

```go
package main

import (
	"flag"
	"fmt"
	"strings"
)

var n = flag.Bool("n", false, "omit trailing newline")
var sep = flag.String("s", " ", "separator")

func main() {
	flag.Parse()
	fmt.Println(strings.Join(flag.Args(), *sep))
	if !*n {
		fmt.Println()
	}
}
```

- `flag.Bool` creates a new flag variable of type bool.
- it takes three arguments
1. the name of the flag 
2. the variable's default value
3. a message that will be printed if the user provides an invalid argument, or `-h` or `-help`
- the variable `sep` and `n` are pointers to the flag variables, which must be accessed indirectly as `*seq` and `*n`
