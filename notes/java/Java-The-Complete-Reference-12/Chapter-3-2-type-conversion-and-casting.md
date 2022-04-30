# Type Conversion and Casting

> If the two types are **compatible**, then Java will perform the conversion automatically.
> **cast**, performs an explicit conversion between **incompatible** types

## Java's Automatic Conversions

> an **automatic type conversion** will take place if the following two conditions are met:
1. the two types are compatible
2. the destination type is **larger** than the source type.

> if two conditions are met, a **widening conversion** takes place.
- e.g. `int` type is large enough to hold all valid `byte` values.

- there are no automatic conversions from `char` or `boolean`
- `char` and `boolean` are not compatible with each other.


## Casting Incompatible Types.

- **narrowing conversion**
: `int` to `byte`

- **cast**
: conversion between two incompatible types
`(target-type) value`

> If the interger's value is larger than the range of a `byte`, it will be reduced modulo byte's range (256)

- **truncation**
> when a floating-point value is assigned to an integer type, the fractinal component is lost.
- `int a = (int)1.23 // 1`
- `int a = (int)1.56 // 1`
