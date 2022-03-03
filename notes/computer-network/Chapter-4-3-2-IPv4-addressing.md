## IPv4 Addressing

- a host typically has a single link into the network
- the boundary between the host and the physical link is called interface.
- a router has many links
- The boundary between the router and any one of its links is also called an interface.
- a router has multiple interfaces, one for each of its links.
- IP requires each host and router interface to have its own IP address
- IP address is technically associate with an interface, rather than with the host or router containing that interface.

- each IP address is 32-bits long (4 bytes) a total of 2^32 about 4 billion possible IP addresses

- IP address are typically written in dotted-decimal notation
  - 192.32.216.9
  - 11000001 00100000 11011000 00001001

- each interface in the global Internet must have an IP address that is global unique. (except for interfaces behind NATs)

### subnet
> this network interconnecting three host interfaces and one router interface forms a subnet.
> a subnet also called an IP network

### subnet mask
> Ip addressing assigns an address to this subnet.
- 223.1.1.0/24
  - leftmost 24 bits of the 32-bit quantity defines the subnet address.
  - host address 223.1.1.1, 223.1.1.2, 223.1.1.3
  - and host address 223.1.1.4

### The Internet's address assignment strategy
> Classless Interdomain Routing (CIDR - pronounced cider)
- CIDR generalizes the notion of subnet addressing.
- a.b.c.d/x
  - network portion of the IP address or prefix (or network prefix) of the address
    leftmost x bits of the address
- an organization is typically assigned a block of contiguous addresses, a range of addresses with a common prefix
  - only the leading x bits of the address are need to be considered in routers.
  - reduce the size of the forwaring table in these routers.
