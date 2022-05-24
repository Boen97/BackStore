# Floating-Point Numbers

- Go provides two sizes of floating-point numbers, `float32` and `float64`
- their arithmetic properties are governed by the IEEE 754 standard implemented by all modern CPUs
- `math.MaxFloat32`
- `math.MaxFloat64`
- a `float32` provides approximately `6` decimal digits of precision
- whereas a `float64` provides about `15` digits.
- `float64` should be preferred for most purpose 
- because `float32` computations accumulate error rapidly unless one is quite careful.
- and the smallest positive integer that cannot be exactly represented as a `float32` is not large.

```go
var f float32 = 16777216 // 1 << 24
fmt.Println(f == f+1)    // "true"!
```
- floating-point numbers can be written literally using decimals, like this:
`const e = 2.71828`
- digits may be omitted before the decimal point(.707) or after it (1.)
- very small or very large numbers are better written in scientific notation.
- with the letter `e` or `E` preceding the decimal exponent.
```go
const a = 6.02214129e23
const b = 6.62606957e-34
```
- Floating-point values are conveniently printed with Printf’s `%g` verb,
- which choose the most compact representation that has adequate precision

- but for tales of data, the `%e` or `%f`(no exponent) forms may be more appropriate.
- all three verbs allow field width and numeric precision to be controlled.

```go
for x := 0; x < 8; x++ {
    fmt.Printf("x = %d e^x = %8.3f\n", x, math.Exp(float64(x)))
}
```
- `%8.3f`
: three decimal digits of the precision
: aligned in an eight-character field

## positive and negative infinites, and NaN

```go
var z float64
z // 0
-z // -0
1 / z // +Inf
-1 / z // -Inf
z / z // NaN
```

- `math.IsNaN`
- `math.NaN` returns NaN

- testing whether a specific computational result is equal to NaN is fraught with peril 

```go
nan := math.NaN
nan == nan // false
nan < nan // false
nan > nan // false
```

- if a function that returns a floating-point result might fail.
- it's better to report the failure separately:

```go
func compu() (value float64, ok bool) {
	failed := false
	if failed {
		return 0, false
	}
	return 1, true
}
```

## floating-point graphics computation
