## Determining the best routes.

> BGP attributes - AS-PATH and NEXT-HOP
- when router advertises a prefix across a BGP connection, it includes with the prefix serveral BGP attributes.
- in BGP jargon, a prefix along with its attributes is called a route.
- two of the more important attributes are AS-PATH and NEXT-HOP

NEXT-HOP
- is the IP address of the router interface that begins the AS-PATH

From AS1 to x, each router in AS1 becomes aware of two BGP routes to prefix x:
- IP address of leftmost interface for router 2a; AS2 AS3;x
- IP address of leftmost interface for router 3d; AS3;x
> hear, each BGP route is with three components: NEXT-HOP;AS-PATH;destination prefix;

### Hot Potato Routing
- we are now finally in position to talk about BGP routing algorithms in a precise manner.
- we will begin with one of the simplest routing algorithm: hot potato routing.

> in hot potato routing, the route chosen is that route with the least cost to the NEXT-HOP router beginning that route.
> the idea behind hot potato routing is for router 1b to get packets out of its AS as quickly as possible
> without worring about the remaining portions of the path outside of its AS to the destination.
- in the name hot potato routing, because it is burning hot, you want to pass it off to another AS as quickly as possible
- Hot potato routing thus is a selfish algorithm, it tries to reduce the cost in its own AS while ignoring the other components of the end-to-edn costs outside its AS.
- with hot potato routing, two routers in the same AS may choose two different AS paths to the same prefix.

### Route-selection algorithm
> in practice, BGP uses an algorithm that is more complicate than hot potato routing, but nevertheless incorporates hot potato routing.
- the input into BGP's route-selection algorithm is the set of all routes to that prefix.
- if there is only one route, then BGP use that route.
- if there are two or more routes to the same prefix.
: the router with the highest local preference value are selected.
  - the value of local preference is a policy decision that is entriely up to the AS's network administrator.
: from the remain routes (with the same highest local preference value), the route with the shortest AS-PATH is selected.
: all with the same highest local preference and the same AS-PATH length, hot potato routing is used.

