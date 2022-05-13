# Reading and Writing Files
> introduce the basic techniques that read from and write to a file.
- `FileInputStream(String fileName) throws FileNotFoundException`
- `FileInputStream(String fileName) throws FileNotFoundException`
> when an output file is opened, any preexisting file by the same name is destroyed.

> **security manager**
- JDK17 deprecates the security manager for removal
- By default, applications run via java do not use a security manager. 
- when a security manager is present, **FileInputStream** and **FileOutputStream** will throw a **SecurityException**

> **when you done with a file, you must close it**
- `void close( ) throws IOException`
> closing a file releases the system resources allocated to the file, allowing them to be used by another file.
> failure to close a file can result in **memory leaks** because of unused resources remaining allocated
> **close()** method is specified by the **AutoCloseable** interface in **java.lang.AutoCloseable**
> **AutoCloseable** interface inherited by the **Closeable** interface in **java.io**
> both **AutoCloseable** and **Closeable** interface are implemented by the stream class.

## two basic approaches to close a file

1. traditional approach
- **close()** is called explicitly when the file is no longer used.

2. **try-with-resources** added by JDK7
- which automatically closes a file when it is no longer needed.

## read from a file
> **FileInputStream.read()**
: each time `read()` is called, it reads a single byte from the file and returns the byte as an integer value.
: `read()` returns -1 when an attempt is made to read at the end of the stream.
: **EOF** end of file

```java
  public static void main(String[] args) {
    FileInputStream fis;
    int i;
    if (args.length <= 0) {
      System.out.println("Please input a filename");
      return;
    }
    try {
      fis = new FileInputStream(args[0]);
    } catch (FileNotFoundException e) {
      System.out.println("FileNotFound");
      return;
    }

    try {
      do {
        i = fis.read();
        if (i != -1)
          System.out.print((char) i);
      } while (i != -1);
    } catch (IOException e) {
      System.out.println("Error Reading File");
    }

    try {
      fis.close();
    } catch (IOException e) {
      e.printStackTrace();
      System.out.println("Error Close File");
    }
  }
```

## variation call `close()` within a `finally` block
```java
  public static void main(String[] args) {
    FileInputStream fis;
    int i;
    if (args.length <= 0) {
      System.out.println("Please input a filename");
      return;
    }
    try {
      fis = new FileInputStream(args[0]);
    } catch (FileNotFoundException e) {
      System.out.println("FileNotFound");
      return;
    }

    try {
      do {
        i = fis.read();
        if (i != -1)
          System.out.print((char) i);
      } while (i != -1);
    } catch (IOException e) {
      System.out.println("Error Reading File");
    } finally {
      try {
        fis.close();
      } catch (IOException e) {
        e.printStackTrace();
        System.out.println("Error Close File");
      }
    }
  }
```
> one advantage with `finally` is that the accessed file terminate the file whether or not the file is terminated by `IOException` or not

> its easier to wrap the portion of the program that open the file
```java
  public static void main(String[] args) {
    FileInputStream fis = null;
    int i;
    if (args.length <= 0) {
      System.out.println("Please input a filename");
      return;
    }
    try {
      fis = new FileInputStream(args[0]);
      do {
        i = fis.read();
        if (i != -1)
          System.out.print((char) i);
      } while (i != -1);
    } catch (FileNotFoundException e) {
      System.out.println("FileNotFound");
    } catch (IOException e) {
      e.printStackTrace();
    } finally {
      try {
        if (fis != null)
          fis.close();
      } catch (IOException e) {
        e.printStackTrace();
      }
    }
  }
```

> a bit more compact version, eliminate the `FileNotFoundException`
```java
  public static void main(String[] args) {
    FileInputStream fis = null;
    int i;
    if (args.length <= 0) {
      System.out.println("Please input a filename");
      return;
    }
    try {
      fis = new FileInputStream(args[0]);
      do {
        i = fis.read();
        if (i != -1)
          System.out.print((char) i);
      } while (i != -1);
    } catch (IOException e) {
      e.printStackTrace();
    } finally {
      try {
        if (fis != null)
          fis.close();
      } catch (IOException e) {
        e.printStackTrace();
      }
    }
  }
```

## write to a file
