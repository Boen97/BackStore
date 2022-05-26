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

## Unicode

### ASCII

- long ago, only one character set to deal with: `ASCII`, the American Standard Code for Information Interchange
- `ASCII` or more precisely `US-ASCII`
- use `7` bits to represent `128` 
- the upper- and lower-case letters of English, digits, and a variety of punctuation and device-control characters. 

- With the growth of the Internet, data in myriad languages has become much more common.

### Unicode
- collects all of the characters in all of the world's writing system
- assign each one a standard number called a `Unicode code point` or in Go, a `rune`

- Unicode version 8 defines code points for over 120,000 characters in well over 100 languages and scripts.

- the natural data type to hold a `single rune` is `int32` and that's what Go uses.

- we could represent a sequence of runes as a sequence of `int32` values.
- in this representation, which is called `UTF-32` or `UCS-4`
- the encoding of each Unicode code point has the same size, 32 bits.
- this is simple and uniform, but it uses much more space than neccessary
- since most computer-readable text is in ASCII
- which requires only 8 bits or 1 byte per character

-  All the characters in widespread use still number fewer than 65,536, which would fit in 16 bits

### UTF-8

- UTF-8 is a variable-length encoding of Unicode code points as bytes. 
- UTF-8 was invented by Ken Thompson and Rob Pike, two of the creators of Go, and is now a Unicode standard.
- it uses between `1` and `4` bytes to represent each rune.
- but only `1 byte` for ASCII characters
- only 2 or 3 bytes for most runes in common use.
- the high order bits of the first byte of the encoding for a rune indicate how many bytes follow.

- A high-order `0` indicates 7-bit ASCII, where each rune takes only `1` byte
- a high-order `110` indicates that the rune takes 2 bytes

- A variable-length encoding precludes direct indexing to access the n-th character of a string,
- but UTF-8 has many desirable properties to compensate.

- Go source files are always encoded in UTF-8, and UTF-8 is the preferred encoding for text strings manipulated by Go programs.
- the `unicode` package provides functions for working with individual runes.
- the `unicode/utf8` package provides functions for encoding and decoing runes as bytes using UTF-8

### Unicode escapes

- Many Unicode characters are hard to type on a keyboard or to distinguish visually from sim- ilar-looking ones; some are even invisible.
- Unicode escapes in Go string literals allow us to specify them by their numeric code point value. 
- There are two forms, 
1. \uhhhh for a 16-bit value
2. \Uhhhhhhhh for a 32-bit value.
- where each h is a hexadecimal digit; 

- Each denotes the UTF-8 encoding of the specified code point.
```go
"BF" 
"\xe4\xb8\x96\xe7\x95\x8c" 
"\u4e16\u754c" 
"\U00004e16\U0000754c"
```

- Unicode escapes may also be used in rune literals.

```go
'B' 
'\u4e16' 
'\U00004e16'
```

- A rune whose value is less than 256 may be written with a single hexadecimal escape, 
- such as '\x41' for 'A', but for higher values, a \u or \U escape must be used.

## string operations

> Thanks to the nice properties of UTF-8, many string operations don’t require decoding. 

```go
func HasPrefix(s, prefix string) bool {
	return len(s) >= len(prefix) && s[:len(prefix)] == prefix
}
func HasSuffix(s, suffix string) bool {
	return len(s) >= len(suffix) && s[len(s)-len(suffix):] == suffix
}
func Contains(s, substr string) bool {
	for i := 0; i < len(s); i++ {
		if (HasPrefix(s[i:], substr)) {
			return true
		}
	}
	return false
}
```

- if we really care about the individual Unicode characters, we have to use other mechanisms.
- s := "Hello, 世界"
: the `s` contains `13 bytes`, but interpreted as `UTF-8`, it encodes only `nine code points or runes`

```go
s := "Hello, 世界"
fmt.Println(len(s)) // 13
fmt.Println(utf8.RuneCountInString(s)) // 9
```
- to process those characters, we need a `UTF-8` decoder

```go
for i := 0; i < len(s); {
    r, size := utf8.DecodeRuneInString(s[i:])
    fmt.Printf("%d\t%c\n", i, r)
    i += size
}
```
- each call to `DecodeRuneInString` returns `r`, the rune itself, and `size`, the number of bytes occupied by the UTF-8 encoding of `r`
- the `size` is used to update the byte index `i` of the next rune in the string.

- Go's `rang loop`, when applied to a string, performs `UTF-8` decoding implicitly

```go
for i, r := range s {
    fmt.Printf("%d\t%q\t%d\n", i, r, r)
}
```

- we could use a simple `range loop` to count the number of `runes` in a string.

```go
n := 0
for range s {
    n++
}
```
