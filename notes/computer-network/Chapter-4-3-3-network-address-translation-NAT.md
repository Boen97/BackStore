## Network Address Translation (NAT)

> a simpler approach to address allocation 

- private network or a realm with private addresses

> NAT-enabled router
1. hiding the details of the home network from the outside world.
   - all traffic leaving the home router or entering the home router all has the same desitination address

2. the router runs a DHCP server to provide addresses in the home networks.
   - NAT-DHCP-router-controlled home network's address space.
   
> NAT translation table

- all datagrams arriving at the NAT router from the WAN have the same destination IP address
- how does the router know the internal host to which it should forward a given datagram?
  - NAT translation table at the NAT router
  - and to include port numbers as well as IP addresses in the table entries.

- when NAT received datagram from a client in the home network
  1. generate a new source port number and replace the old source port number in the datagram
  2. replace the source address with its WAN-side IP address
  3. insert the mapping entry to its NAT transation table
  | WAN side  | LAN side  |
  |:-:|:-:|
  | 138.76.29.7,5001  |  10.0.0.1, 3345 |
  4. port number field are 16-bits long
     - the NAT protocol can support over 60,000 simultaneous connections with a single WAN-side IP address for the router!

> NAT arguments
1. port number are meant to be used for addressing processes, not for addressing hosts
2. peers in a P2P protocal need to accept incoming connections when acting as a servers
   1. How can one peer connect to another peer that is behind a NAT server, and has a DHCP-provided NAT address
   2. Technical solutions to these problems include **NAT traversal tools**
3. the router are meant to be layer 3 (network layer) devices, should process packets only up to the network layer
4. host should be talking directly with each other, without interfering nodes modifying IP addresses, much less port numbers.

#### Inspecting datagrams: firewalls and intrusion detection systems(IDSs)

1. firewalls
- most access routers today has firewall capability
- firewall inspect the datagram and segment header fields, denying suspicious datagrams
- a firewall could be configured to block all ICMP echo request packets, preventing port scan
- firewalls can also block packets based on source and destination IP addresses and port numbers
- firewalls can be configured to track TCP connections, granting entry only to datagrams that belong to approved connections.

2. IDS
- “deep packet inspection,” examining not only head- er fields but also the payloads in the datagram
- An IDS has a database of packet signatures that are known to be part of attacks.

3. IPS
- An intrusion prevention system (IPS) is similar to an IDS, except that it actually blocks packets in addition to creating alerts.
     
