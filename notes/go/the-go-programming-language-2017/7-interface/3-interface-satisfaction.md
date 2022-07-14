# Interface Satisfaction

> a type satisfies an interface if it possesses all the methods the interface requires.

## empty interface type

`interface{}`

- the empty interface type places no demands  on the types that satisfy it
- we can assign `any value` to the empty interface

## type assertion

- of course, having created an interface{} value containing a boolean, float, string, or other types,
- we can do nothing directly to the value it holds since the interface has no methods.
- we need `type assertion`

