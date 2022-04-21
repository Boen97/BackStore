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

#### Channel Partitioning Protocols

- TDM (Time Division Multiplexing)
  - TDM divides time into **time frames** and further divides each time frame into N **time slots**
  - when a node has a packet to send, it transimits the packet's bits during its assigned time slot
  - **fair, each node gets R/N bps transmission rates during each time frame**
  - **drawbacks**
    1. a node is limited to an average rate of R/N bps even when it is the only node with packets to send.
    2. node must always wait for its turn in the transimission sequence, even when it is the only node with a frame to send.
  
- FDM (Frequency division multiplexing)
  - FDM divides the Rbps channel into different frequencies (each with a bandwidth of R/N) and assigns each frequency to one of the N nodes.
  - a node is limited to a bandwidth of R/N, even when it is the only node with packet to send.
  
- **CDMA (code division multiple access)**
  - assigns a different code to each node.
  - each node then uses its unique code to encode the data bits it sends.
  - if the codes are chosen carefully, CDMA network have the wonderful property
  - that different nodes can transmit simultaneously yet have their respective receivers.
  - **CDMA has been used in military systems for some time (due to its anti-jamming properties)**
  - **now CDMA has wide-spread used in cellular telephony**

#### Random Access Protocols

- in a random access protocol, a transmitting node always transmit at full rate of the channel.
- when there is a collision, each node involved in the collision repeatedly retranmits its frame until its frame gets through without a collision.
- **when a node experiences a collision, it don't retransmit right away, it waits a random delay before retransmit the frame**

- **most commonly used random access protocols**
1. ALOHA protocols
2. CSMA protocols (the carrier sense multiple access protocol)
   **Ethernet is a popular and widely deployed CSMA protocol**

##### Slotted ALOHA

- **retransmitting with probability p**
- the event heads corresponds to “retransmit,” which occurs with prob- ability p.
- **Slotted ALOHA allows a node to transimit continuously at the full rate, R, when the node is the only active node.**
- **Slotted ALOHA is highly decentralized, because each node detects collisions and independently decides when to retransmit**
- **Slotted ALOHA requires the slots to be synchronized in the nodes**
