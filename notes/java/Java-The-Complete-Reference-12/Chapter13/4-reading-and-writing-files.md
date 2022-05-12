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
