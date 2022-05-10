# Type Annotations
> annotations can be specified in which a type is used
> you can annotate the return type of a method, the type of this within a method, a cast, an inherited class and a throws clause
> you can also annotate generic types

> a type annotation must include **ElementType.TYPE_USE** as a targe

`void myMeth() throws @TypeAnno NullPointerException { // ...}`


> You can also annotate the type of **this** (called the **receiver**). 
`int myMeth(@TypeAnno SomeClass this, int i, int j) `
> If this is not declared, it is still implicitly passed, as it always has been.
> **If you do declare this, it must be the first parameter.**
> explicitly declaring this does not change any aspect of the method’s signature because this is implicitly declared, by default. 
> you will declare this only if you want to apply a type annotation to it.

```java
// Annotate the return type.
public @TypeAnno Integer f2(int j, int k) {
return j+k; 
}
// Annotate the method declaration.
public @Recommended Integer f3(String str) {
  return str.length() / 2;
  
}
// Annotate the type (in this case String), not the field.
@TypeAnno String str;
// This annotates the field test.
@EmptyOK String test;

public int f(@TypeAnno TypeAnnoDemo<T> this, int x) {} // this is specified as the first parameter and is of type TypeAnnoDemo (which is the class of which f( ) is a member).
```
