> **automatic resource management (ARM)**
- JDK7 added **ARM** feature to manage resources
- forgetting to close a file can result in memory leaks, and could lead to other problems.
```java
try (resource-specification) {

}
```
- **resource-specification** is a statement that declares and initializes a resource, such as a file stream.
- when the `try` block ends, the resouce is auto released.
- `try-with-resouces` statement can also include `catch` and `finally` clauses.

- begin with JDK9, it is possible for the resouce-specification of the `try` to consist of a variable
- that has been declared and initialized earlier in the program.
- however, that variable must be **effectively final**,
- which means that it has not been assigned a new value after being given its initial value.

> the `try-with-resources` statement can be used only with those resources that implement the `AutoCloseable` interface defined by `java.lang`
> `AutoCloseable` interface is inherited by the `Closeable` interface in `java.io`
> thus, `try-with-resouces` can be used with streams, including file streams.

> a resource declared in the `try` statement is implicitly `final`

```java
  public static void main(String[] args) {
    if (args.length <= 0) {
      System.out.println("please input a filename");
      return;
    }
    try (FileInputStream fin = new FileInputStream(args[0])) {
      int i;
      do {
        i = fin.read();
        if (i != -1)
          System.out.print((char) i);
      } while (i != -1);
    } catch (IOException e) {
      e.printStackTrace();
    }
  }
```

> you can manage more than one resource within a single `try` statement

```java
  public static void main(String[] args) {
    try (var fin = new FileInputStream(args[0]);
        var fos = new FileOutputStream("output.txt")) {
      int i;
      do {
        i = fin.read();
        if (i != -1)
          fos.write(i);
      } while (i != -1);
    } catch (FileNotFoundException e) {
      e.printStackTrace();
    } catch (IOException e) {
      e.printStackTrace();
    }
  }
```

> **when using `try-with-resouces`**, the second exception is **suppressed**
- in general, when a try block executes, it is possible that an exception inside the try block
- will lead to another exception that occurs when the resouce is closed in a `finally` clause.
- the original exception is **lost**, being **preempted** by the second exception.
- however, with `try-with-resouces`, **the second exception is suppressed**, it is not lost.
- it is added to the list of suppressed exceptions associated with the first exception.
- the list of suppressed exceptions can be obtained by using the `getSuppressed()` definded by `Throwable`
