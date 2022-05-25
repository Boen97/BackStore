- Go provides two sizes of complex numbers, `complex64` and `complex128`
- whose components are `float32` and `float64` respectly

```go
	var x complex128 = complex(1, 2)
	var y complex128 = complex(3, 4)
	fmt.Println(real(x))
	fmt.Println(imag(y))
```

- if a floating-point literal or decimal integer literal is immediately followed by `i`
- such as `3.141592i` or `2i`, it becomes an `imaginary literal`, denoting a complex number with a `zero` real component

- Under the rules for constant arithmetic, complex constants can be added to other constants
- allowing us to write complex numbers naturally,

- Complex numbers may be compared for equality with == and !=.
- Two complex numbers are equal if their real parts are equal and their imaginary parts are equal.

- the `math/cmplx` package provides library functions for working with complex numbers


