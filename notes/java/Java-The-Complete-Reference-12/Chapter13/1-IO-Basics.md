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
