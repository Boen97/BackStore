# Native Methods.

> you may want to call a subroutine that is written in a language other that Java.
> typically, such a subroutine exists as executed code for the CPU and environment in which you are working--that is, **native code**

> Java provides the **native** keyword, which is used to declare native code methods.
> once declared, these methods can be called from inside your Java program just as you call any other Java method.

> to declare a native method, precede the method with `native`, but do not define any body for the method.

```java
public native int meth();
```
> after you declare a native method, you must write the native method and follow a rather complex series of steps to link it with your Java code.
