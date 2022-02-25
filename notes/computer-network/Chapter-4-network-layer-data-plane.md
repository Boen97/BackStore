> there is a piece of the network layer in each and every host and router int the network.

> distinguish between data-plane and control-plane functions is an important concept.

### overview of Network Layer.

> The primary data-plane role of each router is to forward datagrams from its input links to its output links;

> the primary role of the network control plane is to coordinate these local, per-router forwarding actions 
> so that datagrams are ultimately transferred end-to-end, along paths of routers between source and destination hosts.

- routers do not run applicaton and transport layer protocols.

#### Forwarding and Routing: The Data and Control Planes

> the primary role of network layer is to move packets from a sending host to a receiving host.

- so two important network-layer functions can be identified:
1. **Forwarding**
   - when a packet arrives at a router's input link, the router must move the packet to the appropriate output link.
   - local, per-router forwarding actions which at The Data Planes
   
   > Forwarding refers to the router-local action of transferring a packet from an input link interface to the appropriate output link interface.
   > Forwarding takes place at very short timescales (typically a few nanoseconds), and thus is typically implemented in hardware.
   
   > forwarding is just like getting through a single interchange
   
   - **forwarding table**
     Forwarding is the key function performed by the data-plane functionality of the network layer.

2. **Routing**
   - Routing is implemented in the control plane of the network layer
   - determine the route or path taken by packets from a sender to a receiver.
   - Routing Algorithm - the algorithms that calculate these paths

   > Routing refers to the network-wide process that determines the end-to-end paths that packets take from source to destination. 
   > Routing takes place on much longer timescales (typically seconds), and as we will see is often implemented in software
   
   > Routing is like planning the road of all trip, just like a map.
    
##### Control Plane: The Traditional Approach

- how a router's forwaring table are configured in the first place?
  > This is a crucial issue, one that exposes the important interplay between **forwarding(in data plane)** and **rouring (in control plane)**

- the routing algorithms determines the content of the router's forwarding tables.

- with this traditional approach
> a routing algorithm runs in each and every router
> both forwarding and routing functions are contained within a router.
- the routing algorithm function in one router communicates with the routing algorithm in other routes to compute the values for its forwarding table.
- how router algorithm communicate with each other in different routers.
  by exchanging routing messages containing routing information according to a routing protocol.
- routing protocol
  1. suppose a network in which all forwarding tables are configured directly by human operators at each router.
  2. the human operators need to interact with each other.

##### Control Plane: The SDN Approach
> a physically separate, remote controller computes and distributes the forwarding tables to be used by each router.

- How might the routers and the remote controller communicate?
> By exchanging messages containing forwarding tables and other pieces of routing information. 

> software-defined networking (SDN)
- where the network is “software-defined” because the controller that computes forwarding tables and interacts with routers is implemented in software






 
   


