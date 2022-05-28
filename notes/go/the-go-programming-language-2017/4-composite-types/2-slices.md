# Slices

> slices represents variable-length sequences whose elements all have the same type.

- a slice type is written `[]T`, looks like an array type without a size.

- arrays and slices are intimately connected.
: a slice is a lightweight data structure that gives access to a `subsequence` (or perhaps all) of the elements of an array.
: which is known as the slice's `underlying array`

- a slice has three components
1. a pointer
: the pointer points to the first element of tha array that is reachable through the slice
: which is not necessarily the array's first element.

2. a length
: the length is the number of the slice elements
: it can't exceed the capacity
: `len` function

3. a capacity
: which is usually the number of elements between the `start of the slice` and the `end of the underlying array`
: `cap` function return this value

- multiple slices can share the same underlying array and may refer to overlapping parts of that array

```go
months := [...]string{1: 'January', ..., 12: "December"}
Q2 := months[4:7]
summer := months[6:9]
```

- you can extends a slice `within capacity`

```go
endlessSummber := summer[:5]
```

- since a slice contains a pointer to an element of an array
- passing a slice to a function permits the function to modify the underlying array elements
- in other words, copying a slice creates an `alias` for the underlying array
```go
fun reverse(s []int) {
    for i, j := 0, len(s) - 1; i < j; i, j = i + 1, j - 1 {
        s[i], s[j] = s[j], s[i]
    }
}
```

### slice literal

```go
s := []int{0,1,2,3,4,5}
```

- a `slice literal` looks like an array literal, but the `size` is not given

### slices are not comparable

- unlike arrays, slices are not comparable, so we cannot use `==` to test whether two slices contain the same elements
- the standard library provides highly optimized `bytes.Equal` function for comparing two slices of bytes(`[]byte`)
- but for other types of slice, we must the the comparision ourselves:

```go
func equal(x, y[]string) bool {
    if (len(x) != len(y)) {
        return false
    }
    for i := range x {
        if x[i] != y[i] {
            return false
        }
    }
    return true
}
```

- there are two reasons why deap equivalence is problematic:

1. unlike array elements, the elements of a slice are indirect, making it possible for a slice to contain itself
2. because slice elements are indirect, a fixed slice value may contain different elements at different times 
   as the contents of the underlying array are modified
: because a hash table such as Go's map type makes only `shadow copies` of its keys.
: it requires that equality for each key remain the same throughout the lifetime of the hash table.
: `deep equivalence` would thus make slices unsuitable for use as `map keys`
: for reference type like `pointer` and `channels`, the `==` tests `reference identity`, whether the two entites refer to the same thing

> the safest choice is to disallow slice comparisons altogether.

> the zero value of a slice type is `nil`
- the `nil slice` has length and capacity zero
- but there are also `non-nil slices of length and capacity zero`
- such as `[]int{}` or `make([]int, 3)[3:]`

- as with any type that can have `nil` values, 
- the `nil value` of a slice type can be written such as `[]int(nil)`

```go
var s []int // len(s) = 0, s = nil
s = nil // len(s) = 0, s = nil
s = []int(nil) // len(s) = 0, s = nil
s = []int{} // len(s) = 0, s != nil
```

## make slice function

```go
make([]T, len)
make([]T, len, cap) // same as make([]T, cap)[:len]
```
- under the hood, `make` creates an `unnamed array variable` and returns `a slice of it`
- the array is accessible only through the returned slice.
