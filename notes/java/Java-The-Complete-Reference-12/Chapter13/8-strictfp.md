> with the creation of Java2, the floating-point computation model was relaxed slightly.
> specifically, the new model did not require the truncation of certain intermediate values that occur during a computation.
> this prevented overflow or underflow in some cases.

> by modifying a class, a method, or interface with `strictfp`
> you could ensure that floating-point calculations (and thus all truncations) took place precisely as they did in earlier versions of Java.

> when a class modified by `strictfp`, all the methods in the class were also `strictfp` automatically.

> However, begin with JDK17, all floating-point computations are now strict
> and `strictfp` is obsolete and no longer required.

> Frankly, most programmers never needed to use strictfp, because it affected only a very small class of problems.
