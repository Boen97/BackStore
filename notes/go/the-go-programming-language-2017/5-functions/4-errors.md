- success is not assured because it depends on factors beyond the programmer's control.
- any function that does `I/O`, must confront the possibility of error.

> failure is just one of several expected behaviors.

> Go's `error` are `ordinary values`, not `exceptions`

## Go's error design
- `exceptions` tend to entangle the `description of an error` with `the control flow required` to handle it.
- often leading to an undesirable outcome.
- `routine errors` are reported to the end user in the form of an `incomprehensible stack trace`,
- full of information about the `structure of the program` but leaking `intelligible context about what went wrong`

> by contrast, Go use ordinary control-flow like `if` and `return` to response to errors.
> This style undeniably demands that more attention be paid to `error-handling-logic`, which is `most important`
