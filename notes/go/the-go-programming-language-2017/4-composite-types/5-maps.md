# Maps

- the hash table is one of the most ingenious and versatile of all data structures
- unordered collection of key/value pairs in which all the keys are distinct
- the value of a given key can be retrieved, updated, or removed using a constant number of key comparisons,
- no matter how large the hash table

- in Go, a `map` is a reference to a hash table, and a map type is `map[K]V`
- all of the keys in a given map are of the same type, all of the values are of the same type.

- the key type `K` must be `comparable` using `==`, so that the map can test whether a given key is equal to another
- it's bad idea to compare floats for equality

## create a map

`ages := make(map[string]int)`

### map literal

```go
ages := map[string]int{
    "alice": 31,
    "rhyme": 25,
}
```

- this is equivalent to 
```go
ages := make(map[string]int)
ages["alice"] = 31
ages["rhyme"] = 25
```

- empty map is `map[string]int{}`

## remove element, built in `remove` function

`delete(ages, "alice")`

## safety

- all of the operations are `safe` even if the element isn't in the map.
- a map lookup using a key that isn't present return the `zero value` for its type

## shorthand assignment

```go
ages["rhyme"] += 2
ages["rhyme"]++
```

## map element is not a variable, and we cannot take its address

```go
_ = &ages["rhyme"] // compiler error: cannot take address of map element
```

- one reason that we can't take the address of a map element is that growing a map might cause 
- rehashing existing elements into new storage locations, thus potentially invalidateing the address.

## enumerate the map

```go
for name, age := range ages {
}
```
- the order of map iteration is unspecified, and different implementation might use a different hash function,
- leaging to a different ordering

- to enumerate the key/value pair in order, we must sort the keys explicitly

```go
var names []string
for name := range ages {
    names = append(names, name)
}
sort.Strings(names)
for _, name := range names {
    fmt.Println(ages[name])
}
```

## zero value for a map type is `nil`

- storing to a `nil` map causes a panic, you must allocate the map before you can store into it.
```go
ages["hhh"] = 21 // panic: assignment to entry in nil map
```

## access a map element

- if the key is not present on the map, it will return `zero type` of the value.
- sometimes you need to know whether the element was really there or not.

```go
age, ok := ages["bob"]
if !ok {}
```
- you'll often see thest two statements combined

```go
if age, ok := ages["bob"]; !ok {..}
```

## compare maps

- maps cannot be compared to each other, the only legal comparison is with `nil`
- to test whether two map contain the same keys and values, we must write a loop

## set type with map

- Go does not provide s `set` type, but since the keys of a map are distinct, a map can serve this purpose

## map whose keys are slices

> we can define a helper function that map each key to a string

```go
var m = make(map[string]int)
func k(list []string) string { return fmt.Sprintf("%q", list)}
func Add(list []string)  {m[k(list)]++}
```

- the same approach can be used for any non-comparable key type, not just slices.

- the value type of a map can itself be a composite type, such as a map or slice.
