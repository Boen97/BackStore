- ECMAScipt 是 JavaScript 的标准版本，又简称为ES
- ES5 自动2010年起就已经被所有浏览器所支持
- ES6 在2015年提出，增加了许多功能，以及修正了ES5中的不足
- ES6 之后的版本开始按年份命名 ES2016, ES2017, ES2018
- 在使用ES6或之后的版本将自动使用 strict mode
- the core JavaScript defines a minimal API for working with numbers, text, does not include the input or output
- JavaScript need host environment to provide input or output
- JavaScript host environments
  1. web browser
  2. Node
     Node gives JavaScript access to the entire operating system, allowing JavaScript to read or write files

- expression
a phrase of JavaScript that produce a value.

- an expression is something that computes a value but doesn’t do anything: it doesn’t alter the program state in any way. 
- Statements, on the other hand, don’t have a value, but they do alter the state.

- expression 重在表达，computes a value
- statements 重在语句, 是一句完整的话，对实际的代码会产生影响
- the other broad category of statement is control structures, such as conditionals and loops.

- methods
  : when we use functions with objects, we get methods

- Metaprogramming
  : writing libraries of code for other JavaScript programmers to use.

- Types
1. primitive types
   1. number
   2. string
   3. boolean
   4. null
   5. undefined
   6. Symbol
2. object types
   - a object is a collection of properties
   - global object is a special object
   - array
   > ordered collection of numbered values
   > 而普通的对象是由一组 unordered collection of named values
   - Set
   - Map
   - RegExp
   - Error
   - functions and classes are a special kind of object
   
- The JavaScript interpreter **performs automatic garbage collection** for memory management.

- In JavaScript, null and undefined are the only values that methods cannot be invoked on.

- JavaScript’s object types are mutable and its primitive types are immutable. 

- **strict equality operator ===, which does no type conversions.**

### Numbers

- JavaScript 采用 64-bit floating-point formate to represents numbers

- JavaScript Integer represent range
  2^-53 到 2^53
  
- array indexing and bitwise operator 采用 32-bit 整数


     


