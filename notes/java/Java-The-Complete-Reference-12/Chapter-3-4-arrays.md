## one-dimensional Arrays

- `type[] var-name`
  : type is element type, also called **base type**
  : `int[] monthDays;`

- **new** is a specical operator that **allocates memory**
: `arrayVar = new type[size];`
: `monthDays = new int[12]`;

> the elements in the array allocated by **new** will automatically be initialized to 
1. zero (for numberic types)
2. false (for boolean)
3. null (for reference type)

> **in Java, all arrays are dynamically allocated**

> Arrays can be initialized when they are declared.
- **array initializer**
: there is no need to use **new**
: `int[] array = {1,2,3};`

> The Java run-time system will check that all array indexes are in correct range.
> If you access wrong range, you will cause an **run-time error**

## Multidimensional Arrays

> In Java, multidimensional arrays are implemented as arrays of arrays.

`int[][] twoD = new int[4][5];`

> When you allocated memory for a multidimensional array, you need only specify **the memory for the first(leftmost) dimension.**
> you can allocate the remaining dimensional separately.

```java
int[][] twoD = new int[4][];
twoD[0] = new int[5];
twoD[1] = new int[5];
twoD[2] = new int[6];
...
```
- you do not need to allocate the same number of elements for each dimension
- **uneven (or irregualer) multidimensional arrays**

> initialize multidimensional array
```java
double[][] m = {
    {1, 2},
    {2, 3}
};
```

## Alternative Array Declaration Syntax

```java
int a1[] = new int[3];
int []a2 = new int[4];
```
