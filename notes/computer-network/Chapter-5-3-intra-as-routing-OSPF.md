## Intra-as routing in the Internet: OSPF

> problems that could happen
1. Scale
   - Internet consists of hundreds of millions of routers.
   - storing information for possible destinations at each of these routers would clearly require enormous amounts of memory.
   - The overhead required to broadcast connectivity and link cost updates among all of the routers would be huge.
   - A distance-vector algorithm that iterated among such a large number of routers would surely never converge.
   - **something must be done to reduce the complexity of route computation in a network as large as the Internet**
2. Administrative autonomy
   - the Internet is a network of ISPs.
   - with each ISP consisting of its own network of routers.
   - An ISP generally desires to operate its network as it pleases.
   - an organization should be able to operate and administer its network as it wishes
   - while still being able to connect its network to other outside networks.

> Both of these problems can be solved by organizing routers into **autonomous systems (ASs)**
> with each AS consisting of a group of routers that are under the same administrative control.
