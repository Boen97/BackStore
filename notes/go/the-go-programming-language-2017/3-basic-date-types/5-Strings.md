# Strings

- a string is an immutable sequence of `bytes`
- text strings are conventionally interpreted as `UTF-8-encoded` sequence of `Unicode code points (runes)`
- `len` returns the number of bytes (not runes) in a string.
- and the index `s[i]` retrieves the i-th byte of string s.

- the `i-th` byte of a string is not necessarily the i-th character of a string.
- because the UTF-8 encoding of a non-ASCII code point requires two or more bytes.

## substring

- `s[i:j]` yields a new string consisting of the bytes of the original string straring at index i, and not including index j
- either or both of the `i` and `j` operands may be omitted.
- 0 and len(s) are the default values.

- `+` makes a new string

## compare string

- strings may be compared with `==` and `<`
- the comparion is done byte to byte
- so the result is the natural lexicographic ordering.

## immutable

- string values are immutable
- the byte sequence contained in a string value can never be changed
- though of course, we can assign a new value to a string variable
- try to midfy a string's data in place are not allowed
- `s[0] = 'L'` compile error

> immutability means that it is safe for two copies of a string to share underlying memory
> making it cheap to copy strings of any length

> similarly, a string `s` and a substring like `s[7:]`
> may safely share the same data.
> so the underlying substring operation is also cheap

> no new memory is allocated in either case.

## string literals

- because Go source file are always encoded in UTF-8
- and Go text strings are conventionally interpreted as UTF-8
- we can include Unicode code points in string literals

### escape sequence

- within a double-quoted string literal, `escape sequence` that begin with `\` can be used 
- to insert arbitrary byte values into the string.

- one set of escapes handles ASCII control codes like newline, carrige return and tab:
1. \a alert or bell
2. \b backspace
3. \f form feed 换页
4. \n newline
5. \r carriage return 
6. \t tab
7. \v vertical tab
8. \' singel quote (only in the rune literal '\'')
9. \" double quote (only within "..." literal)
10. \\ backslash

- arbitrary bytes can also be included in literal strings using `hexadecimal` or `octal escapes`
- a hexadecimal escape is written `\xhh`, with exactly two hexadecimal digits `h` (in upper or lower case)
- a octal escape is written `\ooo` with exactly three octal digits `o` not exceeding `\377`

### raw string literal

- a raw string literal is written `....` 
- within a raw string literal, no escape sequence are processed.
- so a raw string literal may spread over several lines in the program source.
- The only processing is that carriage returns are deleted so that the value of the string is the same on all platforms,
- including those that conventionally put carriage returns in text files.

- raw string literals are a convenient way to write `regular expressions`
- which tend to have lots of backslashes.

- they are also useful for HTML templates, JSON literals, command usage messages, and the like which often extends over multiple lines.

```go
const GoUsage = `Go is a tool for managing Go source code.
Usage:
    go command [arguments]
`
```
