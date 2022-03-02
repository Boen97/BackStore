## switching can be accomplished in a number of ways:

### Switching via memory

- earliest routers
  1. traditional computers
  2. switching between input and output ports through the CPU (routing processor)
  3. an input port with an arriving packet first signaled the rouing processor via an memory
  3. the packet was then copied from the input port into processor memory
  4. the routing processor extract the destination address from the header, lookup output port through forwaring table
  5. then copy the packet to the output port
  6. two packets cannot be forward at the same time, since only one memory read/write can be done at a time over the shared system bus
  
### switching via a bus
1. an input port transfer a packet directly to the output port over a shared bus, without intervention by the routing processor.
2. the input port pre-pend a switch-internal label(header) to the package and transmiiting the packet onto the bus
3. all output receive the packet, but only the port that matches the label will keep the packet
4. the label is removed at the output
5. only one packet can cross the bus at a time
6. the switching speed of the router is limited to the bus speed, this is as if the roundabout could contain only one car at a time.
7. switching via a bus is often sufficient for routers that operate in small local area and enterprise networks.
  
### switching via an interconnection network.

1. 
