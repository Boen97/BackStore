> when tow threads hava a **circular dependency** on a pair of synchronized object

> one thread enters the monitor on object X
> anther thread enters the monitor on object Y
> thread in X tries to call any synchronized methods in Y
> thread in Y tries to call any synchronized methods in X

> in general, deadlock occurs rarely, when the two threads time-slice in just the right way.
> deadlock involve more than two threads and two synchronized objects
