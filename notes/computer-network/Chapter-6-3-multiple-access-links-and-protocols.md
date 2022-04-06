## Multiple Access links and Protocols

- two types of network links
1. point-to-point links
2. broadcast links

- broadcast links, can have multiple sending and receiving nodes all connected to the same, single, shared broadcast channel.
- the channel broadcasts the frame and each of the other nodes receives a copy.

> Ethernet and wireless LANs are examples of broadcast link-layer technologies

> How to coordinate the access of multiple sending and receiving nodes to a shared broadcast channel - **the multiple access problem**

> Broadcast channels are often used in LANs, networks that are geographically concentrated in a single building

- television is a one-way broadcast, one fiexed node transimittion to many receiving nodes.
- nodes on a computer network can both send and receive.

### a good anology of broadcast

> a classroom - where teachers and students share the same, single, broadcast classroom.

> **a central problem is that of determing who gets to talk (transimit into the channel)**

### collide

> more than two nodes can transimit frames at the same time.
> all of the nodes receive multiple frames at the same time.
> the transmitted frames collide at all of the receivers.
> all the frames involved in the collision are lost, and the broadcast channel is wasted during the collision interval.

### classify multiple access protocols.

1. channel partitioning protocols
2. random access protocols
3. taking-turns protocols

