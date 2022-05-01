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

## Iteration Statements
1. for
2. while
3. do-while

> the body of the **while** can be empty.
> This is because **null statement** is syntactically valid in Java.

> The do-while loop is useful when you process a menu selection.

```java
char choice;
do {
// choice choose
} while(choice < '1' || choice > '5')
```

### for 

```java
for(initialization;condition;iteration) {
// body
}
```

1. the initialization expression is executed only once.
   : **loop control variable**
2. next, condition is evaluated
3. body of loop
4. next the iteration portion of the loop is executed

#### declaring Loop control variables inside the for loop

> when the variable that controls a for loop is needed only for the loop, we declare the variable inside the portion of the for.
> the scope of that variable ends when the for statement does.

```java
for (int i = 0; i < 10; i++) {
}
```

```java
for (int a = 1, b = 4; a < b; a++, b--) {

}
```

##### some for Loop Variations.

> the initialization, condition test, and the iteration, do not need to be used for only those purposes.

1. the condition expression does not need to test the loop control variable, it can be any boolean expression

2. the initialization and iteration can be absent.

```java
boolean done = false;
for (;!done;) {
}
```

3. infinite loop

```java
for (;;) {
}
```

#### the For-Each Version of the for loop

> a for-each style loop is designed to cycle through a collection of objects, such as an array
> in stricty sequenial fashion, from start to finish.

- for-each style also called **enhanced for loop**

`for(type itrvar: collection)`

> not only the syntax streamlined, but is also prevents boundary errors.
> it is possible to terminate the loop using **break**

> **for-each style, its iteration variable is read-only as it relates to the underlying array**
> **an assignment to the iteration variable has no effect on the underlying array**

#### Iterating over multidimensional arrays

> the enhanced for also works on multidimensional arrays

```java
int[][] nums = new int[5][3];
for (int[] x : nums) {
    for (int y : x) {    
    }
}
```

#### local variable type inference in a for loop

`for (var x : nums)`

## Jump Statements
1. break;
2. continue;
3. return
4. exception handling

### use break
1. terminates a statement sequence in a switch statement
2. exit a loop
3. used as a civilized form of goto

> when used inside a set of nested loops, the break will only break out of the **innermost loop**

1. more than one break statement may appear in a loop
   two many break statements have the tendenct to destructure your code.

2. the break that terminates a switch affects only the switch, not any enclosing loops.

3. break was not designed to provide the normal means by which a loop is terminated. the loop's condition expression serves this purpose.

4. the break statement should be used to cancel a loop only when some sort of special situations.

### using break as a form of goto

> Java does not have a goto statement because it provides a way to branch in an arbitrary and unstructed manner.
> goto makes goto-ridden code hard to understand and maintain.
> prohibits certain compiler optimizations.

> **break label**
- Java defines an expanded form of the break statement
- by using break label, you can break out one or more blocks of code.
- and they can be any block

> you cannot use break to transfer control out of block that does not enclose the break statement

```java
first: {
    second: {
        third: {
            break second;
        }
    }
}
outer: for (int[] i : nums) {
    for (int y : i) {
        break outer;
    }
}
```

## using continue
> in while and do-while loops, a continue statement causes control to be transferred directly to the conditional expression.
> **in a for loop, control goes first to the iteration portion, and then to the conditional expression**

- As with the break statement, continue may specify a label to describe which enclosing loop to continue.

## return

> the return is used to explicitly return from a method, causes program control to transfer back to the caller of the method
