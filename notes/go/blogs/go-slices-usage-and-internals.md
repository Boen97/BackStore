# Go Slices: usage and internals

[Go Slices: usage and internals](https://go.dev/blog/slices-intro)

## Arrays

- the slice type is an abstraction built on top of Go's array

1. fixed size
2. its length is part of its type, `[4]int` and `[5]int` are different type

- arrays do not need to be initialized explicitly.
- the zero value of an array is a `ready-to-use` array whose elements are themselves zeroed.

```go
var a [4]int
a[2] // 0
```

- the `in-memory` representation of `[4]int` is just four integer values laid out `sequentially`

### Go's array are values

> Go's array are `values`

- an array variable denotes the `entire array`
- it is not a pointer to the first array element(as would be the case in C)

> this means that when you assign or pass around an array value you will make a copy of its contents
> to avoid the copy you could pass a pointer to the array, but then that's a pointer to an array, not an array.

> one way to think about arrays is as a sort of struct but with indexed rather than named fields
> a fixed-size composite value.

### Array literals

```go
b := [2]int{2,3}
```

- or you can have the compiler count the array elements for your.

```go
b := [...]int{2,3}
```

## Slices

- the type of slice are `[]T`

## Slice internals

> a slice is a descriptor of an array segment.
> it consists of a pointer to the array, the length of the segment, and its capacity (the maximum length of the segment)

- the length is the number of elements referred to by the slice.
- the `capacity` is the number of elements in the unferlying array, beginning at the element referred to by the slice pointer

- a slice cannot be grown beyond its capacity, but `append` function could
- attempting to do so will cause a runtime panic.

## growing slices (the `copy` and `append` functions)

- to increase the `capacity` of a slice one must create a new, larger slice
- and copy the contents of the original slice into it.
- this techniques is how dynamic array implementations from other language work begind the scenes.

- the next example, doubles the capacity of `s`

```go
t := make([]byte, len(s), (cap(s) + 1) * 2)
for i := range s {
    t[i] = s[i]
}
s = t
```

- `func copy(dst, src []T) int`
- `copy` function supports copying between slices of different lengths, it will copy only up to the smaller number of elements
- `copy` can handle source and destination slices that `share the same underlying array`, handling overlapping slices correctly

```go
a := []int{1,2}
b := []int{3,4}
a = append(a, b...) // append(a, b[0], b[1])
```

## A Possible "gotcha"

- `re-slicing` a slice doesn't make a copy of the underlying array.
- the full array will be kept in memory until it is no longer referenced

> when only a small piece of array is needed, it will cause the program to hold all the data in memory.

- for example, loads a file into memory, and returning a small piece of slices

```go
var digitRegexp = regexp.MustCompile("[0-9]+")

func FindDigits(filename string) []byte {
    b, _ := ioutil.ReadFile(filename)
    return digitRegexp.Find(b)
}
```

- the returned `[]byte` points into an array containing the entire file.

- to fix this problem, we can `copy the interesting data` to a new slice before returning it.

```go
func CopyDigits(filename string) []byte {
    b, _ := ioutil.ReadFile(filename)
    b = digitRegexp.Find(b)
    c := make([]byte, len(b))
    copy(c, b)
    return c
}
```
