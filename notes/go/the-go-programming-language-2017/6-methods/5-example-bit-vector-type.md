# Example: Bit Vector Type

- `Sets` in Go are usually implemented as a `map[T]bool`
- where `T` is the element type.

## bit vector

- a `bit vector` uses a slice of unsigned integer values
- or words, each bit of which represents a possible element of the set
- the set contains `i` if the `i-th` bit is set
