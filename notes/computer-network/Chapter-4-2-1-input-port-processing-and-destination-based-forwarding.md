### Input port processing and destination based forwarding.

- The forwarding table is copied from the routing processor to the line cards over a separate bus (e.g., a PCI bus) indicated by the dashed line from the routing processor to the input line cards

- avoiding a centralized processing bottleneck.

- longest prefix matching rule
> the router matches a prefix of the packet's destination address with the entries in the table.

- the lookup must be performed in nanoseconds.
  1. performed in hardware
  2. fast lookup algorithms
  3. memory access times
     - in practice, TCAMs(Ternary Contenct Addressable Memories) are often used for lookup.
     - With a TCAM, a 32-bit IP address is presented to the memory, which returns the content of the forwarding table entry for that address in essentially constant time.
     - The Cisco Catalyst 6500 and 7600 Series routers and switches can hold upwards of a million TCAM forwarding table entries
     
- a packet may be temporarily blocked from entering the switching fabric
  - if packets from other input ports are currently using the fabric

- a blocked packet will be queued at the input port and then scheduled to cross the fabric at a later point in time

- actions in input processing
1. lookup 
2. physical and link layer processing
3. the packet's version number, checksum, and time-to-live field must be checked
   - the checksum and time-to-live field must be rewritten
4. counters used for network management(such as the number of IP datagrams received) must be updated.

- **match plus actions** abstraction
1. lookup (match) forwarding table entries
2. forward to the ougoing link
   - link-layer and firewalls and NAT(network address translate) are also performed `match plus action`
   


