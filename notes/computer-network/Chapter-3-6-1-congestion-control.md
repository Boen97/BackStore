> packet loss are typically results from the overflowing of router buffes as the network becomes congested.

> packet retrasmission thus treats a symptom of network congestion (the loss of a specific transport-layer segment) 
> but does not treat the cause of network congestion-too many sources attempting to send data at too high a rate.

> to treat the cause of network congestion, mechanisms are needed to throttle senders in the face of network congestion.

### The Causes and Costs of Congestion

#### three increasingly complex scenarios in which congeston occurs.
> focus on the simpler issue of undertanding what happens as the host increase their transmission rate and the network becomes congested.

1. Scenario 1: Two Senders, a Router with Infinite Buffers.
> one of the cose of congestion: larget queuing delays are experienced as the packet-arrival rate nears the link capacity.

- suppose Host A, and Host B share a outgoing link of capacity R
- Host A and Host B is sending data to the connection at an average rate of a bytes/sec
- The router has buffers that allow it to store incoming packets when the packet-arrival rate exceeds the outgoing link's capacity.
- Host A and Host B max per-connection throughput is R/2
- the average delay becomes larger and larger as the sending rate approaches R/2.

2. Scenario 2: Two Senders and a Router with Finite Buffers.

> packets will be droped when arriving to an already-full buffer. and the sender will eventually retransmit it.

> the retransmitted segment will taken the link capacity

> cost of congestion: unneeded retranmissions by the sender in the face of large delays may cause a router to use its link bandwidth to forward
> unneeded copies of a packet.

3. Four Senders, Routers with Finite Buffers, and Multihop paths.

> another cost of congestion: dropping a packet due to congestion, when a packet is dropped along the path, the transmission capacity that
> was used at each of the upstream links to forward that packet to the point at whick it is dropped ends up having been wasted.
