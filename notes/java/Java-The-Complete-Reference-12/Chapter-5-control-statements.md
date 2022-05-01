# Control Statements
1. selection
2. iteration
3. jump

## switch
- the switch statement is Java's multiway branch statement.
- beginning with JDK14, the switch has been significantly enhanced end expanded.
- switch support byte, short, int, char or an enumeration, or String
- **break**, jump out of the switch
- **if you omit the break, execution will continue on into the next case.**

> switching on strings can be more expensive that switching on integers.
> it is best to switch on strings only in cases in which the controlling data is already in string form.
> don's use strings in switch unnecessarily.

> when Java compiler compiles a **switch** statement, the Java compiler will inspect each of the case constants,
> and create a **jump table** that it will use for selecting the path of execution depending on the value of the expression.

> If you need to select among a large group of values, a **switch** statement will run much faster than the **if-elses**
> The compiler can do this because it konws that the case constants are all the same type.
