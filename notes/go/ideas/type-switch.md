# Type switch

```go
package main

import "fmt"

func do(i interface{}) {
	switch v := i.(type) {
	case string:
		fmt.Println("string")
	case int:
		fmt.Println(v * 2)
	default:
		fmt.Println("Rhyme")
	}
}

func main() {
	do("Rhyme")
	do(43)
}
```
