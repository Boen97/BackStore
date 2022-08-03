# Function values

- functions are `values` too, they can be passed around like other values.
- function values may be used as function arguments and return values.

```go
func compute(fn func(a, b int) int) func(int, int) int {
	return fn
}
```

## Function closures

- a `closure` is a `function value` that `references variables from outside its body`.

- for example, the `addr` returns a `closure`, each `closure` is bound to its own `sum` variable

```go
func adder() func(int) int {
    sum := 0
    return func(x int) int {
        sum += x
        return sum
    }
}

func main() {
    pos, neg := adder(), adder()
    for i := 0; i < 10; i++ {
        fmt.Println(pos(i), neg(-2 * i))
    }
}
```

- 注意以下这个例子与上面这个例子的区别

```go
package main

import "fmt"

var sum = 1

func hello() func(int) int {
	return func(x int) int {
		sum += x
		return sum
	}
}

func main() {
	a, b := hello(), hello()
	fmt.Println(a(1), b(2)) // 2, 4
}
```

- 上面的代码，由于引用的是 package level 的变量
- 在执行 `sum += x` 时，处理的是 package level 的 sum
