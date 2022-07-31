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
