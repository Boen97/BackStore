## IPv6
> the 32-bit IPv4 address space was beginning to be used up

- The point in time when IPv4 addresses would be completely allocated was the subject of considerable debate. 

> what happened to IPv5?
- It was initially envisioned that the ST-2 protocol would become IPv5, but ST-2 was later dropped.

### IPv6 Datagram Format

1. Expanded addressing capabilities.
   - IPv6 increases the size of the IP address from 32 to 128 bits. every grain of sand on the planet can be IP-addressable.
   - In addition to unicast and multicast addresses, IPv6 has anycase address.
   - **anycast address**
     - allows a datagram to be delivered to any one of a group of hosts.
     - this feature can be used to send an HTTP GET to the nearest of a number of mirror sites that contain a given document.

2. A streamlined 40-byte header
   - fix-length header allows for faster processing of the IP datagram by a router.
   - A new encoding of options allows for more flexible options processing.
   
3. Flow labeling
   - IPv6 has an elusive definition of a flow
   - the designers of IPv6 foresaw the eventual need to be able to differentiate among the flows
   - For example, audio and video transmission might likely be treated as a flow
   - such as file transfer and e-mail, might not be treated as flows
   - traffic carried by a high-priority user might also be treated as a flow
   
> IPv6 datagram has simpler and more streamlined structure.

4. Version.
   - This 4-bit field identifies the IP version number.
   - IPv6 carries a value of 6 in this field
   - putting a 4 in this field does not create a valid IPv4 datagram.

5. Traffic class.
   - like the TOS field in IPv4, can be used to give priority to certain datagrams within a flow.
   - can be used to give priority to datagrams from certain applications.
     - (for example, voice-over-IP) over datagrams from other applications (for example, SMTP e-mail).

6. Payload length.
   - 16-bit value
   - treated as an unsigned integer giving the number of bytes in the IPv6 datagram following the fixed-length, 40-byte datagram header.

7. Next header.
   - use the same values as the protocal field in the IPv4 header
   - identifies the protocol to which the contents (data field) of this datagram will be delivered (for example, to TCP or UDP).

8. Hop limit.
   - decremented by one by each router that forwards the datagram.
   - if the hop limit reaches zero, a router must discard that datagram.
   
9. Source and destination addresses.
   - IPv6 128-bits address.

10. Data.
    - payload portion of the IPv6 datagram.
    

### fields appearing in the IPv4 datagram and no longer present in the IPv6 datagram.

1. Fragmentation/reassembly
   - if an IPv6 datagram received by a router is too large to be forwarded over the outgoing link.
   - the router simply drops the datagram and sends a "packet too big" ICMP error message.
   - the sender can then resend the data, using a smaller IP datagram size.
   - Fragmentation and reassembly is a time-consuming operation.
   - removing this functionality from the routers and placing it squarely in the end systems speeds up IP forwaring within the network.

2. Header checksum.
   - since IPv4 header contains a TTL field, the header checksum needed to be recomputed at every router.
   - the recomputed is a costly operation.
   - the transport-layer and link-layer protocals performs checksumming.

3. Options.
   - the options field has not gone away in the IPv6
   - the options field is one of the possible next headers pointed to from within the IPv6 header.
   - just as TCP or UDP protocol headers can be the next header within an IP packet, so too can an options field.
   

### Transitioning from IPv4 to IPv6

> new IPv6 capable systems can be made backward-compatible, can send, route, and receive IPv4 datagrams.
> already deployed IPv4-capable systems are not capable of handling IPv6 datagrams.

1. One option would be to declare a flag day
- a given time and date when all Internet machines would be turned off and upgraded from IPv4 to IPv6.
- A flag day involving billions of devices is even more unthinkable today.

2. tunneling
> The approach to IPv4-to-IPv6 transition that has been most widely adopted in practice involves tunneling

- tunnel
> the interventing set of IPv4 routers between two Ipv6 routers as a tunnel.
- with tunneling, the IPv6 node on the sending side of the tunnel 
- takes the entire IPv6 datagram and puts it in the data (payload) field of an IPv4 datagram
- This IPv4 datagram is then addressed to the IPv6 node on the receiving side of the tunnel 
- The IPv6 node on the receiving side of the tunnel eventually receives the IPv4 datagram ((it is the destination of the IPv4 datagram)
- determines that the IPv4 datagram contains an IPv6 datagram (by observing that the protocol number field in the IPv4 datagram is 41



