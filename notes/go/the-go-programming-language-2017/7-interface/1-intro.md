# Inteface

- interface let us write functions that are more flexible and adaptable
- because they are not tied to the details of one particular implementation

> what makes Go's interfaces so distinctive is that they are `satisfied implicitly`

- on other words, there's no need to declare all the interfaces that a given concrete type satisfies.
- simply processing the necessary methods is enough.

> this design lets you create new interfaces that are satisfied by existing concrete types
> without changing the existing types.
> which is useful for types defined in packages that you don't control

## Interface as Contracts

- when you have a value of a `concrete type`, you know exactly what it is and what you can do with it.
- there is another kind of type in Go, called an `interface type`
- `interface type` only reveals some of their methods
