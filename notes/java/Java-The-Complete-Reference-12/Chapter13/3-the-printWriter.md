# The PrintWriter Class

- `PrintWriter(OutputStream outputStream, boolean flushingOn)`
: **flushingOn** controls whether Java flushes the output stream every time a println() method is called.
: if flushingOn is false, flushing is not automatic.

```java
    PrintWriter printWriter = new PrintWriter(System.out, true);
    printWriter.println("Hello PrintWriter");
```
