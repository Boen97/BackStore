## what's inside a router

> forwaring function
- the actual transfer of packets from  a router's incoming links to the appropriate outgoing links at that router.

### High-level view of a generic router.

#### Four Router Components

##### 1. Input ports
1. port
   pysical input and ouput router interfaces, not the software ports
   
2. performs the physi- cal layer function of terminating an incoming physical link at a router;

3. An input port also performs link-layer functions needed to interoperate with the link layer at the other side of the incoming link;

4. a lookup function is also performed at the input port;
   - It is here that the forwarding table is consulted to determine the router output port to which an arriving packet will be forwarded via the switching fabric.

5. the number of ports supported by a router.
   1. enterprise router, small number of ports
   2. ISP's edge router, hundreds of 10 Gbps ports

##### 2. Switching fabric
- connects the router's input ports to its output ports
- completely contained within the router - a network inside of a network router.

##### 3. Output ports
> An output port stores packets received from the switching fabric 
> and transmits these packets on the outgoing link by performing the necessary link-layer and physical-layer functions.

##### 4. Routing Processor
> The routing processor performs control-plane functions.

- In traditional routers, it executes the routing protocols
  - maintains routing tables and attached link state information, and computes the forwarding table for the router
  
- In SDN routers, the routing processor is responsible for communicating with the remote controller 
  - in order to (among other activities) receive forwarding table entries computed by the remote controller, 
  - and install these entries in the router’s input ports.
  
- The routing processor also performs the network management functions

### why input ports, ouput ports, switching fabric are implemented in hardware.

- with a 100 Gbps input link and a 64-byte IP datagram, the input port has only 5.12 ns to process the datagram before another datagram may arrive.
- If N ports are combined on a line card
- the datagram-processing pipeline must operate N times faster—far too fast for software implementation.

### a router’s control functions

- operate at the millisecond or second timescale.
- These control plane functions are thus usually implemented in software and execute on the routing processor (typically a traditional CPU).

### when a car enters the roundabout

> packet forwarding was compared to cars entering and leaving an interchange.
> as a car enters the roundabout, a bit of processing is required.

1. Destination-based forwarding
   - has clear destination address
2. Generalized forwarding
   - datagrams are typed by properties, such as color, brand.

