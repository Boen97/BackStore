## ICMP: The Internet Control Message Protocol

> ICMP is used by hosts and routers to communicate network-layer information to each other.
> the most typical use of ICMP is **error reporting**

- for example, when running an HTTP session, you may have encountered "Destination network unreachable", this message origins in ICMP
- At some point, an IP router was unable to find a path to the host.
- **that router created and send an ICMP message to your host indicating the error**

> ICMP is often considered part of IP, but architecturally it lies just above IP
> ICMP messages are carried as IP payload, just as TCP and UDP segments are carried as IP payload.
- when a host receive an IP datagram with ICMP specified as the upper-layer protocol
- it demultiplexes the datagram's contents to ICMP, just as it would demultiplexes a datagram's content to TCP or UDP.

### ICMP messages
- ICMP messages have a type and a code field,
- and contain the header and the first 8 bytes of the IP datagram that cause the ICMP message to be generated in the first place.
- so the sender can determine the datagram that cause the error
- ICMP messages are not only for signaling error conditions.

### ICMP message types
- ICMP Type Code Desciption
1. 0 0 echo reply(to pinp)
2. 3 0 destination network unreachable
3. 3 1 destination host unreachable
4. 3 2 destination protocol unreachable
5. 3 3 destination port unreachable
6. 3 6 destination network unknown
7. 3 7 destination host unknown
8. 4 0 source quench (congestion control)
9. 8 0 echo request
10. 9 0 router advertisement
11. 10 0 router discovery
12. 11 0 TTL expired
13. 12 0 IP header bad

> the ping program sends an ICMP type 8 code 0 message to the specified host
> the destination host, send back a type 0 code 0 ICMP echo reply.

> traceroute is implemented with ICMP messages
> Traceroute in the source sends a series of ordinary IP datagrams to the destination.
> Each of these datagrams carries a UDP segment with an unlikely UDP port number.
> the first datagram has a TTL of 1, the second of 2, third of 3, and so on
> when the nth datagram arrives at the nth router, the nth router observes that the TTL just expired
> according to the rules of the IP protocol, the router discard the datagram
> and sends an ICMP warning message to the source, which includes the name of the router and its IP address.

- how does a traceroute source know when to stop sending UDP segments?
  : the source increments the TTL fiels for each datagram it sends.
  : one of the datagrams will eventually make it all the way to the desination host.
  : because the datagram contains a UDP segment with an unlikely prot number.
  : the desination host sends a port unreachable ICMP messages (type 3 code 3) back to the source
  : when the source receives this particulaer ICMP message, it knows its end, and no need to send probe packets.
  : The standard Traceroute program actually sends sets of three packets with the same TTL;
  : thus, the Traceroute output provides three results for each TTL.

- a new version of ICMP has been defined for IPv6
- ICMPv6 also added new types and codes required by the new IPv6 functionality. 
- ICMPv6 also added new types and codes required by the new IPv6 functionality. 
