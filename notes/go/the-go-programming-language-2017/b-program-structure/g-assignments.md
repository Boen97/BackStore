# Assignments

```go
x = 1
*p = true
person.name = "bob"
count[x] = count[x] * scale
count[x] *= scale
v := 1
v++ // v = v + 1
v-- // v = v - 1
```

## Tuple Assignment

```go
x, y = y, x
a[i], a[j] = a[j], a[i]
x, y = y, x%y
x, y = y, x%y
i, j, k = 2, 3, 5
f, err = os.Open("foo.txt")  // function call returns two values
```

> all of the right-hand side expressions are evaluated before any of the variables are updated

- we can assign unwanted values to the blank identifier
```go
_, err = io.Copy(dst, src)
_, ok = x.(T)
```
- short variable declaration is different with assignment, so the blank identifier could not be used in short variable declaration
