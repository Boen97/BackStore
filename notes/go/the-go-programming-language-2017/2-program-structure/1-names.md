> go into more detail about the basic structural elements

## name rule

- a name begins with a letter (anything that Unicode deems a letter) or an underscore
- and may have any number of additional letters, digits, and underscores
- case matters

## keywords

- Go has 25 keywords like `if` and `switch` that may used only where the syntax permits.
- they can't be used as names.
: break default func interface select
: case defer go map struct 
: chan else goto package switch
: const fallthrough if range type
: continue for import return var

## predeclared names

- there are three dozen `predeclared names` like `int` and `true` for built-in constants, types, and functions.
- Constants 
: true false iota nil

- Types
: int int8 int16 int32 int64
: unit unit8 unit16 unit32 unit64 unitptr
: float32 float64 complex128 complex64
: bool byte rune string error

- Functions
: make len cap new append copy close delete
: complex real imag
: panic recover

> these names are not reserved, so you may use them in declarations

## entity scope

- if an entity is declared within a function, it is **local** to that function
- if declared outside of a function
- it is visible in all files of the `package` to which it belongs

> the case of the first letter of a name determines its visibility across package boundaries
- if a name begins with an upper-case letter, it is **exported**
- which means that it is visible and accessible outside of its own package and may be referred to by other parts of the program.

> package names themselves are always in lower case.

> Go programs lean toward short names
> especially for local variables with small scopes
- a variable named `i` than `theLoopIndex`

> generally, the larger the scope of a name, the longer and more meaningful it should be.

> use **camel case** when forming names by combining words

> the letters of acronyms and initialisms like `ASCII` and `HTML` are always rendered in the same case.
> so a function might be called htmlEscape, HTMLEscape, or escapeHTML, but not escapeHtml.
