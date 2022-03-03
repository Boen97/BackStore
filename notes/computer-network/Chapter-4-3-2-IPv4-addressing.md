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
  
> the lower order bits may (or may not) have an additional subnetting structure.

#### classful addressing
> Before CIDR was adopted, the network portions of an IP address were constrained to be 8, 16, or 24 bits in length
> since subnets with 8-, 16-, and 24-bit subnet addresses were known as class A, B, and C networks, respectively. 
- The requirement that the subnet portion of an IP address be exactly 1, 2, or 3 bytes long turned out to be problematic for supporting the rapidly growing number of organizations with small and medium-sized subnets. 

- A class C (/24) subnet could accommodate only up to 2^8 - 2 = 254 hosts (two of the 2^8 = 256 addresses are reserved for special use)
  - too small for many organizations

- class B (/16) subnet, which supports up to 65,634 hosts, was too large.
- This led to a rapid depletion of the class B address space and poor utilization of the assigned address space.

- IP broadcast address 255.255.255.255
  - the message is delived to all hosts on the same subnet
  - routers optinally forward the message into neighboring subnets as well (although usually don't)
  
- the route using longest prefix mathcing when has two or more matching items in the forward table.

- address aggregation (also route aggregation or route summarization)
  - Organization 1 200.23.16.0/23
  - Organization 2 200.23.18.0/23
  - Organization 3 200.23.20.0/23
  - the address beginning with 200.23.16.0/20 all match organization 1, 2, 3

### Obtaining a Block of Addresses
- ISP's block: 200.23.16.0/20 11001000 00010111 0001/0000 00000000
- Organization 0: 200.23.16.0/23 11001000 00010111 0001000/0 00000000
- Organization 1: 200.23.16.0/23 11001000 00010111 0001001/0 00000000
- Organization 2: 200.23.16.0/23 11001000 00010111 0001010/0 00000000
......

- IP addresses are managed under the authority of the Internet Corporation for Assigned Names and Numbers (ICANN)

### Obtaining a Host Address: The Dynamic Host Configuration Protocal

> once obtained a block of addresses, it can assign individual IP addresses to the host and router interfaces in its organization.

- IP addresses of the router are typically manually configed by system manager.

> Host address can also be configured manually, but typically is done using DHCP (Dynamic Host Configuration Protocal)

#### DHCP (Dynamic Host Configuration Protocal)
> DHCP allows a host to obtain (be allocated) an IP address automatically.

- DHCP could be configured so that each time a given host receives the same IP address or a temporary IP address

- DHCP allow host to learn additional information
  1. subnet mask
  2. the address of its **first-hop router (often called the default gateway)**
  3. the address of its local DNS server
  
- DHCP also called **plug-and-play** or **zeroconf (zero configuration)** protocal.

- DHCP is a client-server protocal
  
- relay agent
  If no server is present on the subnet, a DHCP relay agent (typically a router) that knows the address of a DHCP server for that network is needed

- For a newly arriving host, the DHCP protocal is a four-step process:
  > yiaddr (your Internet address)

1. DHCP server discovery
   1. first task for a newly arriving host is to find a DHCP server with which to interact
   2. DHCP discover message 
      1. the client send a DHCP discover message within a UDP packet to port 67
      2. the client create an IP datagram
         1. IP address was 255.255.255.255
         2. this host source IP address of 0.0.0.0
         3. this message will be broadcast to all nodes in the subnet

2. DHCP server offer(s)
   1. a DHCP server receiving a DHCP discover message reponds to the client with a DHCP offer message
   2. broadcast to all nodes on the subnet using the IP broadcast address of 255.255.255.255
   3. why this server reply must also be broadcast
      1. since serveral DHCP servers can be present on the subnet, the client may find itself in the enviable position of being able to choose from among several offers.
   4. each DHCP offer message contains: 
      1. transation ID of the received discover message
      2. the proposed IP address for the client
      3. the network mask
      4. an IP address lease time
         - the amount of time for which the IP address will be valid
      
