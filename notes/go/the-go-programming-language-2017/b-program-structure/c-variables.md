# Variables

> `var name type = expression`
- either the `type` or the `= expression` part may be omitted, but not both
- if the `type` is omitted, it is determined by the initializer expression
- if the expression is omitted, the initial value is the `zero value` for the type,
- which is 0 for numbers, false for booleans, "" for strings and nil for interface and reference types
- the zero value of an aggregate type like an array or a struct has the zero value of all its elements or fields.

- the zero-value mechanism ensures that a variable always holds a well-defined value of its type;
- in Go there is no such thing as an uninitialized variable
- this simplifies code and often ensures sensible behaviour of boundary conditions without extra work.
```go
var s string
fmt.Println(s)
```

```go
var i, j, k int
var b, f, s = true, 2.3, "four"
```

- omitting the type allows declaration of multiple variables of different types
- initializers may be literal values or arbitrary expressions.
- package-level variables are initialized before main begins
- local variables are initialized as their declarations are encountered during function execution.

## short variable declaration

> within a function, an alternate form called **a short variable declaration** may be used to declare and initialize local variables

`name := expression`
- the type of name is determined by the type of expression

- because of their brevity and flexibility, short variable declarations are used to declare and initialize the majority of local variables

- a `var` is for a variable that need an explicit type or assign a value later and its initial value is unimportant. 

```go
i := 100
var boiling floate64 = 100
var names []string
var err error
var p Point
i, j := 0, 1
```

- `:=` is a declaration, whereas `=` is an assignment

- a multi-variable declaration should not be confused with a `tuple assignment`
- in which each variable on the left is assigned the corresponding value from the right
`i, j = j, i`

- If some of them were already declared in the same lexical block (§2.7), then the short variable declaration acts like an assignment to those variables.
```go
in, err := os.Open(file)
out, err := os.Create(file)
```
- the first statement declares both in and err. 
- The second declares out but only assigns a value to the existing err variable.

- a short variable declaration must declare at least one new variable

```go
f, err := os.Open(file)
f, err := os.Create(outfile) // compile error
```

- A short variable declaration acts like an assignment only to variables that were already declared in the same lexical block;
- declarations in an outer block are ignored.
