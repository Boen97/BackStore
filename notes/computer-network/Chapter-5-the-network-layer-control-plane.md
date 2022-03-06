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

