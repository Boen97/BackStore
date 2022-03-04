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
    

