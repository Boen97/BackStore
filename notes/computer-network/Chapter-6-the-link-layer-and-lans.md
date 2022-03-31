> how packets are sent across the individual links
> how are transmmission conflicts in broadcast links resolved?
> what exactly the difference between a switch and a router.

> **two fundamentally different types of link-layer channels**
1. broadcast channels
   : connect multiple hosts in wireless LANs
   : in satellite network, and in hybrid fiber-coaxial cable(HFC) access networks.
   : since many hosts are connected to the same broadcast communication channel.
   : a so-called medium access protocol is needed to coordinate frame transmission.
   : in some case, **a central controller** may be used to coordinate
   : in other cases, **the hosts themselves coordinate transmission**
   
2. point-to-point communication links
   : between two routers connected by a long-distance link
   : between a user's office computer and nearby Ethernet switch
   : **PPP Point-to-Point Protocol**
  
- **node**
: any device that runs a link-layer protocol.
: includes hosts, routers, switches, and WIFI access points.

- **links** 
: communication channels that connect adjacent nodes.
   
- **link-layer frame**

> inside the link layer and how it related to network layer.
- transportation analogy
: the travel agent is a routing protocol
: the tourist is a datagram
: each transportation segment is a link
: the transportation mode is a link layer protocol

> it is the responsibility of the airline company or a train company to get the tourist to the desitination place.
> each of the three segments of the trip is **direct between two adjacent locations**
> three transpotation segments are managed by three different companies and use entirely different transpotation modes.

## the services provided by the link layer.
