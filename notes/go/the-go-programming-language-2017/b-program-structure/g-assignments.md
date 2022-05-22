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

## Assignability

- there are many places in a program where an assignment occurs `implicitly`
- a function call implicitly assigns the argument values to the corresponding parameter variables
- a return statement implicitly assigns the return operands to the corresponding result variables
- and a literal expression for a composite type:
- `metals := []string{"a", "b"}`
- implicitly assigns each element
```go
metals[0] = "a"
metals[1] = "b"
```
- An assignment, explicit or implicit, is always legal if the left-hand side (the variable) and the right-hand side (the value) have the same type.
- More generally, the assignment is legal only if the value is assignable to the type of the variable.

- the rules for **assignability** are simple:
: the types must exactly match, and nil may be assigned to any variable of interface or reference type.

- Whether two values may be compared with == and != is related to assignability: 
- in any comparison, the first operand must be assignable to the type of the second operand, or vice versa.
