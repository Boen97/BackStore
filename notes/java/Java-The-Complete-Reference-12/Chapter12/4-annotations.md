# Annotations

> enable you to **embed supplemental information into a source file**
> does not change the actions of a program
> an annotation leaves the semantics of a program unchanged
> **the information can be used by various tools during both development and deployment**

> the term **metadata** is used to refer to this feature
> but the term **annotation** is the most descriptive and more commonly used.

## Annotation Basics

> an annotation is created based on the **interface**

```java
public @interface MyAnno {
  String str();
  int val();
}
```

- **@interface** tells the compiler that an annotation type is being declared
- all annotations only have method declarations.
- Java implements these methods
- an annotation cannot include an **extends** clause
- all annotation types automatically extend the **Annotation** interface

> any type of declaration can hava an annotation associated with it
- classes, methods, fields, parameters ...

```java
  @MyAnno(str = "Hello", val = 12)
  public void testAnno() {
  }

```
