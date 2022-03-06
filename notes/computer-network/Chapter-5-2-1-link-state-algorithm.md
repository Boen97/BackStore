## Link-State (LS) algorithm

> the network topology and all link costs are known, available as input to the LS algorithm.

- each node broadcast link-state packets to all other nodes in the network
- with each link-state packet containing the identities and costs of its attacked links.

> link-state broadcast algorithm

- all nodes have an identical and complete view of the network.

### Dijkstra's algorithm
> a link-state algorithm, a closely related algorithm is Prim's algorithm

- D(v)
  - the cost of the lease-cose path from source node to v
- P(v)
  - previous node (neighbor of v) along the current least-cost path from source to v
- N'
  - subset of nodes which the least-cost from source is known.
  
> Link-State (LS) algorithm for source node u
1. Initialization
   ```
   N' = {u}
   for all nodes v
       if v is a neighbor of u
           then D(v) = c(u, v)
       else D(v) = Infinity
   ```
2. Loop
   ```
   find w not in N' such that D(w) is a minimum
   add w to N'
   update D(v) for each neighbor v of w and not in N':
       D(v) = min(D(v), D(w) + c(w, v))
   ```
3. until N' = N
