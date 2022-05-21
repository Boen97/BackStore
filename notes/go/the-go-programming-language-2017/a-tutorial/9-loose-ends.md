# Loose Ends

## switch 

```go
switch coinflip() {
case "heads":
    heads++
case "tails":
    tails++
default:
    fmt.Println("")
}
```

- cases do not **fallthrough** as in C

## tagless switch 

> it's equivalent to `switch true`

```go
func Signum(x int) int {
    switch {
        case x > 0:
            return +1
        default:
            return 0
        case x < 0:
            return -1
    }
}
```

## break continue

> statements may be labeled so that break and continue can refer to them

- there is even a `goto` statement, though it's intended for machine generated code
- not regular use by programmers.

## Named Types

> a type declaration makes it possible to give a name to an existing type.
> since `struct` type are often long, they are nearly always named.

## Pointers

> Go provides pointers, that is ,values that contain the address of a variable
- in Go, Pointers are explicitly visible.
- The `&` operator yields the address of a variable
- The `**` operator retrieves the variable that the pointer refers to
- but there is no pointer arithmetic.

## Methods and interfaces

> a method is a function associated with a named type.
> Go is unusual in that methods may be attached to almost any named type.

> interfaces are abstract types that let us treat different concrete types 
> in the same way based on what methods they have.
> not how they are represented or implemented.

## Packages

> Programming is often more about using existing packages than 
> about writing original code of one's own.

> before you embard on any new program
> it's a good idea to see if packages already exist
> that might help you get your job done more easily.

> `https://golang.org/pkg` 
: standard library packages

> `https://godoc.org`
: packages contributed by the community

> the `go doc` tool makes thest documents easily accessible from the command line.
- `go doc http.ListenAndServe`

## Comments

- it's also a good style to write a comment before the declaration of each function
- thest convertions are important
- because they are used by tools like `go doc` and `godoc` to locate and display documentation.
- `/*..*/` also support
- such comments are sometimes used at the beginning of a file for a large block of 
- explanatory text to avoid a // on every line.
- // and /* has no special meaning within a comment, so comments do not nest.


