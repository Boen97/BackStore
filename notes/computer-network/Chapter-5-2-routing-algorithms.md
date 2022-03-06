## Routing Algorithms

> determine good paths (equivalently routers), from sender to receives, through the network of routers.

> a good path is one that has the least cost

- in real-world concerns such as policy issues
  - as “router x, belonging to organization Y, should not forward any packets originating from the network owned by organization Z ”

- whether the network control plane adopts a per-router control approach or a logically centralized approach
- there must be a well-defined sequence of routers that a packet will cross in traveling from sender to receiver.
- Thus, the routing algorithms that computes these paths are of fundamental importance.

> graph G = (N, E)
- a graph is used to formulate routing problems.
- a set of N of nodes
- a collection E of edges.
- a edge also has a value representing its cost.
  - may reflect the physical length of the corresponding link
  - the link speed
  - or the monetary cost associated with a link.
  - c(x, y) as the cose of the edge between nodes x and y.
  
- least-cost path
- if all edges in the graph have the same cose. the least-cost path is also the **shortest path**

### centralized routing algorithms
> compute the least-cost path between a source and destination using complete, global knowledge about the network.
- This then requires that the algorithm somehow obtain this information before actually performing the calculation.
> the algorithm has complete information about connectivity and link costs.
> LS (link-state algorithm)
- algorithm with global state information are often referred to as link-state (LS) algorithms
- since the algorithm must be aware of the cost of each link in the network.

### decentralized routing algorithm
> the calculation of the least-cost path is carried out in an iterative, distributed manner by the routers.
> No node has complete information about the costs of all network links.
- each node begins with only the knowledge of the costs of its own directly attacked links.
- then through an iterative process of calculation and exchange information with its neighboring nodes
- a node gradually calculates the least-cost path.
> DV (distance vector) algorithm
- because each node maintains a vector of estimates of the costs (distances) to all other nodes in the network.

### static / dynamic routing algorithms
> a second broad way to classify routing algorithms

### load-sensitive or load-insensitive.
> Today’s Internet routing algorithms (such as RIP, OSPF, and BGP) are load-insensitive,
> as a link's cost does not explicitly reflect its current level of congestion.
