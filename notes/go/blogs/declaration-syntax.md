# Go's Declaration Syntax

`f func(func(int,int) int, int) func(int, int) int`

- `from left to right`, and it’s always obvious which name is being declared - the name comes first.
- The distinction between type and expression syntax makes it easy to write and invoke closures in Go:

`sum := func(a, b int) int { return a+b } (3, 4)`

- Go’s type syntax is easier to understand than C’s, especially when things get complicated.

- Go’s declarations read left to right. It’s been pointed out that C’s read in a spiral!
