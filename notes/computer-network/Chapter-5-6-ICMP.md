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
