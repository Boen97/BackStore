# Effective Go

## Formatting

- with Go we take an unusual approach and let the machine take care of most formatting issues.
- the `gofmt` program.

## Commentary

- `//` line comments are the norm.
- block comments appear mostly as package comments, but are useful within an expression or to disable large swaths of code.

## Names

### package names

```go
import "bytes"
```

- it's helpful if everyone using the package can use the same name to refer to its contents
  which implies that the package name should be `good, short, concise, evocative`

- by convention, packages are given `lower case, single-word` names.
- there should be `no need` for underscores or mixedCaps
- Err on the side of brevity, since everyone using your package will be typing that name.
- don't worry about collision a `priori`
- the package name is only the `default name` for imports, it need not be unique across all source code.

- another convention is that the `package name` is the base name of its `source directory`
- the package in `src/encoding/base64` is imported as `encoding/base64`, not `encoding_base64` and not `encodingBase64`

- avoid `repetition`
  such as reader type in the `bufio` package is called `Reader`, not `BufReader`
  `ring.New` not `ring.Ring` or `ring.NewRing`

- long names don't auto make things more readable.
  a helpful doc comment can often be more valuable than an extra long name.
