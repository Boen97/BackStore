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
- Each node involved in a collision chooses independent random delays

- **most commonly used random access protocols**
1. ALOHA protocols
2. CSMA protocols (the carrier sense multiple access protocol)
   **Ethernet is a popular and widely deployed CSMA protocol**

##### Slotted ALOHA

- nodes start to transimit frames only at the beginning of slots
- the nodes are synchronized so that each node knows when the slots begin
- if two or more frames collide in a slot, then all the nodes detect the collision event before the slot ends
- **retransmitting with probability p**
- the event heads corresponds to “retransmit,” which occurs with prob- ability p.
- **Slotted ALOHA allows a node to transimit continuously at the full rate, R, when the node is the only active node.**
- **Slotted ALOHA is highly decentralized, because each node detects collisions and independently decides when to retransmit**
- **Slotted ALOHA requires the slots to be synchronized in the nodes**
- The slotted ALOHA protocol required that all nodes synchronize their transmissions to start at the beginning of a slot. 
- when there are multiple active nodes, a certain fraction of the slots will have collisions and will wasted.
- fraction of the slots will be empty because all active nodes refrain from transimission as a result of the probabilistic transmission policy.
- the only unwasted slots will be those in which exactly one node transmit
- **successful slot**
  : a slot in which exactly one node transmits
- **efficiency**
  : successful slot rates
  : if no form of access control were used, each node were to immediately retransmit after each collision, the efficiency would be zero.
  
- **the maximum efficiency of slotted ALOHA**
  : 1/e = 0.37
  : when a large number of nodes have many frames to transimit, then(at best) only 37 percent of the slots do useful work
  : the effective transimission rate of the channel is only 0.37 R bps

#### Pure ALOHA
: in order for this frame to be successfully transmitted, no other nodes can begin their transmission in the interval of time [t0 - 1, t0]. 
: Such a transmis- sion would overlap with the beginning of the transmission of node i’s frame.
: the maximum efficiency of the pure ALOHA protocol is only 1/(2e)-half of slotted ALOHA
: this then is the price to be paid for a fully decentralized ALOHA protocol

#### CSMA (carrier sense multiple access)

- in both slotted and pure ALOHA, a node's decision to transimit is made independently of the activity of the other nodes attached to the broadcast channel
- ALOHA neither pays attention to whether another node happens to be transimission when it begins transimit
  nor stops transmitting if another node begins to interfere with its transmission

##### Two Rules

- **Listen before speaking**
  : **carrier sense**
    - a node listens to the channel before transimitting
    - if a frame from another node is currently being transmitted into the channel,
    - a node then waits until it detects no transimission for a short amount of time and then begins transmission

- **If someone else begins talking at the same time, stop talking**
  : **collision detection**
    - a transmitting node listens to the channel while it is transmitting
    - if it detects that another node is transmitting an interfering frame
    - it stops transmitting and waits a random amount of time before repeating the sense-and-transmit-when-idle cycle

- the above two rules are embodied in CSMA and **CSMA/CD(CSMA with collision detection)** protocol

- When use CSMA, why if all nodes perform carrier sensing, do collisions occur in the first place
  after all, a node will refrain from transmitting whenever it senses that another node is transmitting
  
  - because **channel propagation delay** of broadcast channel
  : the time it takes for a signal to propagate from one of nodes to another. 
  : the channel propagation delay plays a crucial role in performance

##### CSMA/CD (Carrier Sense Multiple Access with Collision Detection)

- with normal CSMA, nodes do not perform collision detection
- both B and D continue to transmit there frames in their entirely even though a collision has occured
- **When a node performs collision detection, it ceases transmission as soon as it detects a collision**
- **add collision detection will help protocol performance by not transmitting a useless, damaged frame**

###### **binary exponential backoff** algorithm
: used in Ethernet and DOCSIS cable network, solves the random time choose after a collision stop
: when transmitting a frame that has already **experienced n collisions**
: a node chooses the value of **K** at random from **{0,1,2,...2^n-1}**
: thus **the more collisions experienced by a frame, the larger the interval from whick K is choosed**
: **for Eithernet, the actual amount of time a node waits is K*512 bits times**
: for example
  - first time random choose K from {0, 1}
    : when K = 0, wait time = 0 * 512 = 0
    : when K = 1, wait time = 1 * 512 = 512
  - second time ... K from {0, 1, 2, 3}
    : ...

###### CSMA/CD Efficiency
- Efficiency = 1 / (1 + 5(dprop)/dtrans)
- when dprops apporaches 0, the efficiency apporaches 1
- when dtrans becomes very large, the efficiency apporaches 1


### Taking-Turns Protocols

> two desirable properties of a multiple access protocol
1. when only one node is active, the active node has a throughput of R bps
2. when M nodes are active, then each active node has a throughput of R/M bps.

- **the ALOHA and CSMA protocols has the first property but not the second**

#### Polling protocol
- the polling protocol requires one of the nodes to be designated as a **master node**.
- **the master node polls each of the nodes in a round-robin fashion**
- the master node first sends a message to node 1, saying that it (node 1) can transmit up to some maximum number of frames.
- after node 1 transmit some frames, the master node tells node 2 to transimit
- the master node can determine when a node has finished sending its frames by observing the lack of a signal on the channel

- **the polling protocol eliminates the collisions and empty slots that plague random access protocols**

> **drawbacks**
1. introduce a **polling delay**
   : when only one node is active, then the node will transmit at a rate less than R 
2. if the **master node fails**, the entire channel becomes inoperative
   : the Bluetooth protocol, is an example of a Polling protocol

#### Token-passing protocol

> a small, special-purpose frame known as a **token** is exchanged among the nodes in some fixed order.
- for example, node 1 always send the token to node 2, node 2 always send the token to node 3
- **when a node receives a token, it holds onto the token only if it has some frames to transimit**

> **drawbacks**
1. the failure of one node can crash the entire channel

### 6.3.4 DOCSIS: The Link-Layer Protocol for Cable Internet Access

> three broad classes of multiple access protocols
1. channel partitioning protocols
2. random access protocols
3. taking turns protocols

- we’ll find aspects of each of these three classes of multiple access protocols with the cable access network!

> **DOCSIS (Data-Over-Cable Service Interface Specifications)**

- **DOCSIS uses FDM to divide the downstream (CMTS to modem) and upstream network segments into multiple frequency channels**

- each downstream channel is between 24 MHz and 192 MHz wide, maximum 1.6 Gbps per channel
- each upstream between 6.4 MHz to 96 MHz, with a maximum upstream throughput of approximately 1 Gbps.

> **each upstream and downstream is a broadcast channel**

> **there is no multiple access problem, since there only a single CMTS transmitting into the downstream channel**

> **each upstream channel is divided into intervals of time (TDM like)**
- each containing a sequence of mini-slots during which cable modems can transmit to the CMTS
- The CMTS explicitly grants permission to indi- vidual cable modems to transmit during specific mini-slots.
- The CMTS accomplishes this by sending a control message known as a MAP message on a downstream channel 
- to specify which cable modem (with data to send) can transmit during which mini-slot for the interval of time specified in the control message.
- Since mini-slots are explicitly allocated to cable modems, the CMTS can ensure there are no colliding transmissions during a mini-slot.

> how does the CMTS know which cable modems have data to send in the first place?
- This is accomplished by having cable modems send mini-slot-request frames to the CMTS during a special set of interval mini-slots 
- that are dedicated for this purpose, 
- These mini-slot-request frames are transmitted in a **random access manner** and so may collide with each other.
  : A cable modem can neither sense whether the upstream channel is busy nor detect collisions. 
  : the cable modem infers that its mini-slot-request frame experienced a collision if it does not receive a response to the requested allocation in the next downstream con- trol message.
  : When a collision is inferred, a cable modem uses binary exponential backoff
