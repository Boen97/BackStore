# The Type Promotion Rules

> Java defines several **type promotion rules** that apply to expressions

1. all `byte`, `short`, `char` values are **promoted** to `int`
2. if one operand is a `long`, the whole expression is promoted to `long`
3. if one operand is `float`, the entire expression is promoted to `float`
4. if `double`, is promoted to `double`

```java
byte b = 42;
char c = 'a';
short s = 1024;
int i = 5000;
float f = 5.67f;
double d = .1234;
double res = (f * b) + (i / c) - (d * s);
```

1. (f * b) b is promoted to float
2. (i / c) c is promoted to int
3. (d * s) s is promoted to double
...
