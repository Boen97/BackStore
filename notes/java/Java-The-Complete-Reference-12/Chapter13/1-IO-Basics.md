> **java.io**

# I/O Basics
> Java's I/O system is cohesive and consistent
> once you understand its fundamentals, the rest of the I/O system is easy to master

## Streams
> Java programs perform I/O through streams
> **a stream is an abstraction that either produces or consumes information**
> a stream is linked to a physical device by the Java I/O system
> all streams behave in the same manner, even if the actual physical devices which they are linked differ
> this means an input stream can abstract many different kinds of input

> in addition to the stream-based I/O defined in **java.io**
> Java also provides **buffer-and channel-based I/O**, which is defined in **java.nio**

### Byte Streams and Character Streams
> Java defines two types of I/O streams: **byte and character**

> **Byte streams**  provide a convenient means for handling input and output of **bytes**
- byte streams are used, for example, when reading or writing binary data

> **Character streams** provide a convenient means for handling input and output of **characters**
- they use **Unicode**, and therefore, can be **internationalized**
- in same cases, character streams are more efficient than byte streams

> as a general rule, old code should be updated to take advantage of character streams where appropriate.

> **at the lowest level, all I/O is still byte-oriented**
> the character-based streams simply provide a convenient and efficient means for handling characters

#### The Byte Stream Classes
> defined using two class hierarchies, at the top are two abstract classes: **InputStream** and **OutputStream**
> to use the stream classes, you must import **java.io**

1. BufferedInputStream
2. BufferedOutputStream
3. ByteArrayInputStream
   : input stream that reads from a byte array
4. ByteArrayOutputStream
   : output stream that writes to a byte array
5. DataInputStream
   : an input stream that contains methods for reading the Java standard data types
6. DataOutputStream
   : an output stream that contains methods for writing the Java standard data types
7. FileInputStream
   : input stream that reads from a file
8. FileOutputStream
   : output stream that writes to a file
9. FilterInputStream
   : implements InputStream
10. FilterOutputStream
    : implements OutputStream
11. InputStream
    : abstract class that describes stream input
12. ObjectInputStream
    : input stream for objects
13. ObjectOutputStream
    : output stream for objects
14. OutputStream
    : abstract class that describes stream output
15. PipedInputStream
    : Input pipe
16. PipedOutputStream
    : Output pipe
17. PrintStream
    : output stream that contains **print()** and **println()**
18. PushbackInputStream
    : input stream that allows bytes to be returned to the input stream
19. SequenceInputStream
    : input stream that is a combination of two or more input streams
    : that will be read sequentially, one after the other

#### The Character Stream Classes
