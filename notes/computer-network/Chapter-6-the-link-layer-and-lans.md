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

1. Framing
2. Link access (**medium access(MAC) protocol**)
   : specifies the rules by which a frame is transimitted onto the link.
   : for point-to-point link, the MAC protocol is simple
   : the sender can send a frame whenever the link is idle.
   : for broadcast link, the MAC protocol is used to coordinate the frame transimittion.
   
3. Reliable delivery.
   : a link-layer delivery service is often used for links that prone to high error rates, such as a wireless link.
   : many wired link-layer protocols do not provide a reliable delivery service.

4. Error detection and correction.
   : bit errors often occured in signal attenuaton and electromagetic noise.
   : having transimitting node inclued error-detection bits in the frame.
   : having the receiving node perform an error check.
   : error detection in the link layer is implemented in hardware.

## where is link layer implemented?

: for the most part, the link layer is implemented on a chip called the **network adapter**
: **network adapter** somtimes known as **network interface controller (NIC)**
: much of a link-layer controller's functionallity is implemented in hardware.
