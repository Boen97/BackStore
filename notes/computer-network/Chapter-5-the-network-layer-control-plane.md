## The Network Layer: Control Plane

> The network-logic that controls not only how a datagram is routed along an end-to-end path from the source host to destinaton host
> but also how network-layer components and services are configured and managed.

- Internet routing protocols
1. OSPF
- is a routing protocol that operates within a single ISP's network.
2. BGP
- is a routing protocol that serves to interconnect all of the networks in the Internet.

- SDN (software-defined network) makes a clear separation between the data and control planes
- control-plane functions in a separate controller service
- the router controls the forwaring components

- ICMP (the Internet Control Message Protocal)

- SNMP (Simple Network Management Protocal)

> the forwarding table (destination-based forwarding) and the flow table (generalized forwarding) 
> were the principle elements that linked the network layer's data and control plane.
> these tables specify the local data-plane forwarding behaviour of a router.

> how those forwaring and flow tables are computed, maintained and installed.
1. Per-router control
   - a routing algorithms runs in each and every router.
   - both a forwaring and routing functions are contained within each router.
   - each router has a routing component that communicat with other routing components in other routers to compute the values for its forwaring table.
   - the OSPF and BGP protocols are based on this per-router approach to control.
   
2. Logically centralized control.
   - a logically centralized controller computes and distribute the forwarding tables to be used by each and every router.
   - the generalized match-plus-action abstraction allows the router to perform traditional IP forwarding as well as a rich set of other functions
   - such as load sharing, firewalling, and NAT that had been previously implemented in separate middleboxes.
   - CA (control agent)
   - the controller interacts with a control agent (CA) in each of the routers via a well-defined protocol to configure and manage the flow table.
   - the CA's job is to communicat with the controller and to do as the controller commands.
   - CAs does not directly interact with each other nor do they actively take part in computing the forwaring table.
   - this is a key distinction between per-router control and logically centralized control.

- 75% of our network functions will be fully virtualized and software-controlled.
