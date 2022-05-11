# Repeating Annotations
> Beginning with JDK 8, an annotation can be repeated on the same element. 
> must be annotated with **@Repeatable**
> its value field specifies the **container type** for the repeatable annotation

```java
@Retention(RetentionPolicy.RUNTIME)
public @interface MyRepeatedAnnos {
  MyAnno[] value();
}
@Repeatable(MyRepeatedAnnos.class)
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnno {
  String value();
}
@MyAnno("Hello")
@MyAnno("World")
public void myMeth() {
}
```
```java
public class TestRun {
  @MyAnno("Hello")
  @MyAnno("World")
  public void myMeth() {
  }

  public static void main(String[] args) {
    TestRun t = new TestRun();
    Class<? extends TestRun> c = t.getClass();
    try {
      Method method = c.getMethod("myMeth");
      MyRepeatedAnnos repeat = method.getAnnotation(MyRepeatedAnnos.class);
      for (MyAnno a : repeat.value()) {
        System.out.println(a.value());
      }
    } catch (NoSuchMethodException | SecurityException e) {
      e.printStackTrace();
    }
  }
}
```

> you can use `getAnnotationsByType()` direct get the Repeating Annotation instead the Container Annotation
```java
Annotation[] annos = m.getAnnotationsByType(MyAnno.class);
for(Annotation a : annos)
  System.out.println(a);
```

## Some Restrictions

1. no annotation can inherit another
2. all methods declared by an annotation must be without parameters.
3. annotation methods cannot specify a throws clause.
