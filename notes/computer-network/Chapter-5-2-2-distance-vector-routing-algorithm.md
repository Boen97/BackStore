## The Distance-Vector (DV) Routing Algorithm.

> whereas LS algorithm is an algorithm using global information, the distance-vector(DV) algorithm is iterative, asynchronous, and distributed.

> It is distributed in that each node receives some information from one or more of its directly attached neighbors, 
> performs a caculation, and then distributes the results of its calculation back to its neighbors.

- it is iterative in that this process continues on until no more information is exchanged between neighbors.

- the algorithm is self-termination, there is no signal that the computation should stop.

> the DV algorithm is asynchronous in that it does require all of the nodes to operate in lockstep with each other.

- `dx(y)` is the cost of the least-cost path from node x to node y.

### Bellman-Ford equation.
- `dx(y) = min(v) {c(x,v), dv(y)}`
- v represent the collection of v's neighbors
- `min(v)` taken over all of x's neighbors

> the solution to the Bellman-Ford equation provides the entries in node x's forwaring table

> another important practical contribution of the Bellman-Ford equation is that it suggests the form of the neighbor-to-neighbor communication 
> that will take place in the DV algorithm.
