## array

```go
var a [2]int = [2]int{1,2}
```

## low and high bound

```go
arr := [6]int {1,2,3,4,5,6}
slice := arr[1 : 4]
```


## slices are like references to arrays

- a slice does not store any data, it just describes a section of an 
- underlying array.
- changing the elements of slice modifies the corresponding elements of the array

## slice literals

```go
arr := [2]int{1,2}
s := []int{1,2,3}
ss := []struct {
    name string
    age int
} {
    {"Rhyme", 23},
}
```

## slice defaults

```go
var a [10]int
a[0:10]
a[:10]
a[0:]
a[:]
```

## slice length and capacity

- a slice has both a length and a capacity
- the length of a slice is the number of elements it contains
- the capacity of a slice is the number of elements in the underlying array,counting from the first element in the slice.
- `len(s)` and `cap(s)`

## Nil slices

- the zero value of a slice is `nil`
- a nil slice has a length and capacity of 0 and has no underlying array

```go
var s []int
fmt.Println(s, len(s), cap(s))
if s == nil {
    fmt.Println("nil")
}
```

## creating a slice with make

- slices can be created with `make`, this is how you create `dynamically-sized` arrays
- the `make` allocates a zeroed array and returns a slice that refers to that array

```go
a := make([]int, 5) // len = 5, cap = 5
b := make([]int, 0, 5) // len = 0, cap = 5
```

## slices of slices

```go
a := [][]string{
    []string{"Rhyme", "Chiang"}
}
```

## append to a slice

- If the backing array of s is too small to fit all the given values a bigger array will be allocated

```go
s := []int{}
s = append(s, 2)
```
