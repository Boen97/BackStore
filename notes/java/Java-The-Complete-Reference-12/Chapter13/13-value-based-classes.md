# A word about value-based classes.

> begin with JDK8, Java has included the concept of **value-based classes**
> value-based  classes are defined by various rules and restrictions.
> value-based classes must be `final`, and their instance variables must also be `final`

> if `equals()` determines that two instances of a value-based class are equal
> one instance can be used in place of the other.

> **very importantly, you should avoid using instances of a value-based class for synchronization**
