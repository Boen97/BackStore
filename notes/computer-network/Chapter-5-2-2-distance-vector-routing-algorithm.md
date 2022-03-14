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

- `Dx = [Dx(y): y in N]`
- with the DV algorithm, each node x maintains the following routing information:
  1. for each neighbor v, the cost c(x, v) from x to directly attached neighbor v.
  2. Node x's distance vector, that is, Dx = [Dx(y): y in N], containing x's estimate of its cose to all destinations, y in N.
  3. the distance vectors of each of its neighbors, that is Dv = [Dv(y): y in N] for each neighbor v of x
  
- in the distributed, and asynchronous algorithm, from time to time, each node send a copy of its distance vector to each of its neighbors.
- when a node x receives a new distance vector from any of its neighbor w, it saves w's distance vector, 
- and then use Bellman-Ford equation to update its distance vector
  `Dx(y) = Minv{c(x,v) + Dv(y) }` for each of node y in N
- if node x's distance vector has changed as a result of this update step, node x will then send its updated distance vector to each of its neighbors
- which can be in turn update their own distance vectors
> for node x to update its forwarding table to node y, what node x really need to know is not the shortest-path distance to y
> but instead the neighboring node v*(y) that is the next-hop router along the shortest path to y.

- LS algorithm is a centralized algorithm in the sense that it requires each node to first obtain a complete map of the network before running the Dijkstra algorithm.

- while DV algorithm is decentralized and does not use such a global information.
- indeed, the only information a node will have is the costs of the links to its directly attached neighbors and information it receives from its neighbors.

- DV algorithm are using in may routing protocols in practice, including the Internet's RIP and BGP.


#### A comparison of LS and DV routing algorithm
- The DV and LS algorithms take complementary approaches toward computing routing.
- In the end, neither algorithm is an obvious winner over the other; indeed, both algorithms are used in the Internet.
