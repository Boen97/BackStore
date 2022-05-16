# using assert

> it is used during program development to create an `assertion`, which is a condition that should be true during the execution of the program.

> Assertions are often used during testing to verify that some expected condition is acutally met.
> they are not used for released code.

## two forms of the assert keyword
1. `assert condition;`
   : condition is an Boolean expression
   : if result is true, then the assertion is true and no other action takes place.
   : if result is false, then a default `AssertionError` object is thrown.
   
2. `assert condition:expr;`
   : `expr` is a value that is passed to the `AssertionError` constructor.
   : this value is converted to its string format and displayed if an assertion fails.

> to enable assertion checking at run time, you must specify the `-ea` option.
`java -ea AssertionDemo`

```java
assert n > 0 : "n is not positive";
```

> you must not rely on them to perform any action required by the program.
> released code will be run with assertions disabled.

> Assertions can be quite useful because they streamline the type of error checking that is common during development.

## Assertion Enabling and Disabling Options.

> `-da`
- disable all assertions by using `-da` option

> you can enable or diable a specific package (and all of its subpackages) 
> by specifying its name followed by three periods after the `-ea`, or `-da` option.

- `-ea:MyPack...`
: enable assertions in a package called MyPack

- `-da:MyPack...`
: disable assertions in MyPack

- you can also specify a class with the `-ea` or `-da` option.

