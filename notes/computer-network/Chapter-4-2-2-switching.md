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
  
