# Variables

> `var name type = expression`
- either the `type` or the `= expression` part may be omitted, but not both
- if the `type` is omitted, it is determined by the initializer expression
- if the expression is omitted, the initial value is the `zero value` for the type,
- which is 0 for numbers, false for booleans, "" for strings and nil for interface and reference types
- the zero value of an aggregate type like an array or a struct has the zero value of all its elements or fields.

