# Recursion

- `recursion` is a powerful technique for many problems, and of course it's essential for processing `recursive data structures`

- `golang.org/x/net/html` is a non-standard package, which provides an `HTML` parser
- the `golang.org/x/...` repositories hold packages designed and maintained by the `Go team`
- these packages are not in the standard library because they're still under development or 
- because they're rarely needed by the Go programmers.

- `html.Parse` function reads a sequence of bytes, parses them, and returns the `root of the HTML document tree`, which is an `html.Node`

## Go implementations of `variable-size` stacks

- Go use `variable-size` stacks that start small
- and grow as needed up to a limit on the order of a gigabyte.
- this let us use recursion `safely` and `without worrying about overflow`
