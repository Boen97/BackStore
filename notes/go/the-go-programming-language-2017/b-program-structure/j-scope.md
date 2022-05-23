# Scope

- a declaration associates a name with a program entity, such as a function or a variable
- the `scop` of a declaration is the part of the source code where a use of the declared name refers to that declaration

- don's confuse `scope` with lifetime.
- the scope of a declaration is a region of the program text, it is a `compile-time` property.
- the lifttime of a variable is the range of time during execution it is a `run-time` property.

- A `syntactic block` is a sequence of statements enclosed in braces like those that surround the body of a function or loop.
- A name declared inside a syntactic block is not visible outside that block. 
- The block encloses its declarations and determines their scope. 

- We can generalize this notion of blocks to include other groupings of declarations that are not explicitly surrounded by braces in the source code;
- we’ll call them all `lexical blocks`
- There is a lexical block for the entire source code, called the `universe block`

- A declaration’s lexical block determines its scope, which may be large or small.
- The declarations of built-in types, functions, and constants like int, len, and true 
- are in the universe block and can be referred to throughout the entire program.

- `package-level`
: declarations outside any function

- `file level`
: imported packages, such as `fmt`, are declared at the `file level`
: so they can be referred to from the same file
: but not from another file in the same package without another import

- A program may contain multiple declarations of the same name so long as each declaration is in a different lexical block

- When the compiler encounters a reference to a name
- it looks for a declaration, starting with the `innermost` enclosing lexical block and working up to the universe block.
- If a name is declared in both an outer block and an inner block, the inner declaration will be found first.
- the inner declaration is said to `shadow` or `hide` the outer one, making it inaccessible.

- The for loop above creates two lexical blocks:
1. the explicit block for the loop body, 
2. and an implicit block that additionally encloses the variables declared by the initialization clause, such as i.
- The scope of a variable declared in the implicit block is the condition, post-statement (i++), and body of the for statement.
- Like for loops, if statements and switch statements also create `implicit blocks` in addition to their body blocks.

```go
if x := f(); x == 0 {
         fmt.Println(x)
     } else if y := g(x); x == y {
         fmt.Println(x, y)
     } else {
         fmt.Println(x, y)
     }
     fmt.Println(x, y) // compile error: x and y are not visible here
```

- the second if statement is nested within the first
- so variables within the first statement's initializer are visible within the second.
- similar rules apply to each case of a `switch` statement
- there is a block for the condition and a block for each `case` body

- normal practice in Go is to deal with the error in the if block and then return, so that the successful execution path is not indented.

- Short variable declarations demand an awareness of scope.

```go
 var cwd string
 func init() {
    cwd, err := os.Getwd() // compile error: unused: cwd
        if err != nil {
            log.Fatalf("os.Getwd failed: %v", err)
  } 
}
```
- since neither `cwd` and `err` is already declared in the init function’s block
- the := statement declares both of them as local variables.

```go
var cwd string
     func init() {
         var err error
         cwd, err = os.Getwd()
         if err != nil {
             log.Fatalf("os.Getwd failed: %v", err)
} }
```
