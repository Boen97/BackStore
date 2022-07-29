# Looping construct

- Go has only one looping construct, the `for` loop

1. init statement
2. the condition expression
3. the post statement

- the init statement will often be a short variable declaration
- the variable declared in the init statement are visible only in the scope of the `for` statement
- there are no parentheses surrounding the three components
- the `{}` are always required

- the init and post statement are optional

```go
package main

import "fmt"

func main() {
	sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
}
```
