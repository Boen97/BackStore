## Intra-as routing in the Internet: OSPF

> problems that could happen
1. Scale
   - Internet consists of hundreds of millions of routers.
   - storing information for possible destinations at each of these routers would clearly require enormous amounts of memory.
   - The overhead required to broadcast connectivity and link cost updates among all of the routers would be huge.
   - A distance-vector algorithm that iterated among such a large number of routers would surely never converge.
   - **something must be done to reduce the complexity of route computation in a network as large as the Internet**
2. Administrative autonomy
   - the Internet is a network of ISPs.
   - with each ISP consisting of its own network of routers.
   - An ISP generally desires to operate its network as it pleases.
   - an organization should be able to operate and administer its network as it wishes
   - while still being able to connect its network to other outside networks.

> Both of these problems can be solved by organizing routers into **autonomous systems (ASs)**
> with each AS consisting of a group of routers that are under the same administrative control.

- often the routers in an ISP, and the links that interconnect them, constitude a singel AS.
- some ISPs, however, partition their network into multiple ASs.

> An autonomous system is identified by its globally unique autonomous system number (ASN)
> AS numbers, like IP addresses, are assigned by ICANN regional registries.

> routers within the same AS all run the same routing algorithm and have information about each other.
> the routing algorithm running within an autonomous system is called an **intra-autonomous system routing protocol**

### Open Shortest Path First (OSPF)

> OSPF routing and its closely related cousin, IS-IS, are widely used for intra-AS routing in the Internet.
> the Open in OSPF indicates that the routing protocol specification is publicly available.

> OSPF is a link-state protocol that uses flooding of link-state information and a Dijkstra's least-cose path algorithm.

- with OSPF, each router constructs a complete topological map (that is, a graph) of the entire autonomous system.
- each router then locally runs Dijkstra's shortest-path algorithm to determine a shortest-path tree to all subnets, with itself as the root node.

- individual link costs are configured by the network administrator.
- OSPF does not mandate a policy for how link weights are set, that is the job of the network administrator

- with OSPF, a router broadcast routing information to all other routers in the autonomous system.
- a router broadcast link-state information whenever there is a change in a link's state.
- a router also broadcast link's state periodically (at least once every 30 minutes)

- some of the advances embodied in OSPF including the following:
1. Security.
     - exchange between OSPF routers can be authenticated, only trusted routers can participate in the OSPF protocol within an AS
     - by default, OSPF packets between routers are not authenticated and could be forged.
     - two types of authentication can be configured: simple and MD5
     1. simple authentication
        - the same password is configured on each router.
        - when a router sends an OSPF packet, it includes the password in plaintext
     2. MD5 authentication
        - MD5 authentication is based on shared secret keys that are configured in all the routers.
        - the router computes the MD5 hash of the content of the OSPF packet appended with the secret key.
        - then the router includes the resulting hash value in the OSPF packet.
        - the receiving router, using the preconfigured secret key, will compute an MD5 hash of the packet 
        - and compare it with the hash value that the packet carries, thus verify the packet's authenticity.
        - sequence number are also used with MD5 authentication to protect against replay attacks.
2. Multiple same-cost paths.
   - when multiple paths to a destination have the same cost, OSPF allows multiple paths to be used.

3. Integrated support for unicast and multicast routing.
   - Multicast OSPF (MOSPF) [RFC 1584] provides simple extensions to OSPF to provide for multicast routing.
   - MOSPF uses the existing OSPF link database and adds a new type of link-state advertisement to the existing OSPF link-state broadcast mechanism.

4. support for hierarchy within a single AS
   - an OSPF autonomous system can be configured hierarchically into areas.
   - each area runs its own OSPF link-state routing algorithm.
   - within each area, one or more area border routers are responsible for routing packets outside the area.
   - exactly one OSPF area in the AS is configured to be the backbone area.
   - the primary role of the backbone area is to route traffic between the other areas in the AS
   - the backbone always contains all area border routers.
