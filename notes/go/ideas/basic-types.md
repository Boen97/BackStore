# Basic Types

## the range of `int64`

`- 1 << 63`  ~ `1 << 63 - 1`

- one bit left for sign, so the max bit is 64 - 1 = 63
- 1 << 2 = 100 = 4
- because only one 0, so `1 << 63 - 1`

## int to binary string

`fmt.Sprintf("%b", math.MaxInt)`

## max of `uint8`

- 1 << 8 - 1
- binary is `11111111`
