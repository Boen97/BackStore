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

## Specifying a Retention Policy
> **annotation retention policies**
> a retention policy determines at what point an annotation is discarded
> Java defines three policies, which are defined in **java.lang.annotation.RetentionPolicy**
1. SOURCE
   - retained only in the source file and is discarded during compilation
   
2. CLASS
   - is stored in the .class file during compilation
   - not available through the JVM during the run time.
   
3. RUNTIME
   - stored in the .class file during compilation
   - available through the JVM during the run time.

> an annotation on a local variable declaration is not retained in the .class file

> **@Retention**
> **the default policy is CLASS**

```java
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnno {
  String val();
}
```

## obtaining Annotations at Run Time by Use of Reflection
> Reflection is the feature that enables information about a class to be obtained at run time.
> If retention policy is RUNTIME, they can be queried at run time by any Java program through the use of reflection
> **java.lang.reflect**

### steps to using the reflection

1. obtain a **Class** object that represents the class 
   - **getClass()**

```java
package com.rhyme.app.test5;

import java.lang.reflect.Method;

public class AnnoRun {

  @MyAnno(val = "HelloAnno")
  public static void myMeth() {
    AnnoRun ar = new AnnoRun();
    Class<?> class1 = ar.getClass();
    try {
      Method m = class1.getMethod("myMeth");
      MyAnno annotation = m.getAnnotation(MyAnno.class);
      System.out.println(annotation.val());
    } catch (NoSuchMethodException | SecurityException e) {
      e.printStackTrace();
    }
  }

  public static void main(String[] args) {
    myMeth();
  }
}
```

> **class literal**
- `MyAnno.class`
- you can obtain a class literal for **classes, interfaces, primitive types, and arrays**
```java
int.class
```

```java
  @MyAnno(val = "MyMeth2")
  public static void myMeth2(String name, int val) {
    AnnoRun ar = new AnnoRun();
    Class<?> c = ar.getClass();
    try {
      Method m = c.getMethod("myMeth2", String.class, int.class);
      MyAnno annotation = m.getAnnotation(MyAnno.class);
      System.out.println(annotation.val());
    } catch (NoSuchMethodException e) {
      e.printStackTrace();
    } catch (SecurityException e) {
      e.printStackTrace();
    }
  }
```

## The AnnotatedElement Interface
- getAnnotation()
- getAnnotations()
- getDeclaredAnnotations()
: returns all non-inherited annotations present in the invoking object
- isAnnotationPresent()
- getAnnotationsByType()

## using default values
```java
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnno {
    String str() default "hello";
    int val() default 100;
}
```

## Marker Annotations
> a marker annotation is a special kind of annotation that contains no members
> its sole purpose is to make an item.
> its presence as an annotation is sufficient

```java
@Retention(RetentionPolicy.RUNTIME)
@interface MyMaker {}

@MyMaker // no need ()
public void test() {

}
```

> **AnnotatedElement.isAnnotationPresent()**

## single-member Annotations
> you don't need to specify the name of the member
> in order to use this shorthand, the name of the member must be **value**

```java
@Retention(RetentionPolicy.RUNTIME)
@interface MyMaker{
    int value();
}
```

> you can use the single-value syntax which have other members
> but those members must all have default value

```java
@Retention(RetentionPolicy.RUNTIME)
@interface SomeAnno{
    int value();
    int zyx() default 100;
}
```

> whenever you are using a single-member annotation, the name of that member must be value.
