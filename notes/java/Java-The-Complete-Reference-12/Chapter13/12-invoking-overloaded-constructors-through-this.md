# invoking overloaded constructors through this()

`this(arg-list)`

> the call to `this()` must be the first statement within the constructor.

```java
package com.rhyme.app.test9;

public class TestThis {
  public TestThis(int i) {
  }
  public TestThis() {
    this(0);
  }
}
```

> constructors that call `this()` will execute a bit **slower** than those that contain all of their initialized code inline.
> this is because the call and return mechanism used when the second constructor is invoked adds overhead.

> if you class will be used to create a large number of objects, then the negative impact of the increased overhead could be meaningful.

> for very short constructors, such as those used by MyClass, there is often little difference in the size of the object code whether this( ) is used or not.
> there are cases in which no reduction in the size of the object code is achieved.
> This is because the bytecode that sets up and returns from the call to this( ) adds instructions to the object file. 
> Therefore, in these types of situations, even though duplicate code is eliminated, using this( ) will not obtain significant savings in terms of load time.
> However, the added cost in terms of overhead to each object’s construction will still be incurred. 

> **Therefore, this( ) is most applicable to constructors that contain large amounts of initialization code, not those that simply set the value of a handful of fields.**

- Second, you cannot use super( ) and this( ) in the same constructor because each must be the first statement in the constructor.
