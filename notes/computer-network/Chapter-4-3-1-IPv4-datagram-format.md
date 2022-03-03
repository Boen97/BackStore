## IPv4 Datagram Format

> the datagram plays a central role in the Internet, everyone needs to master it.

### key fields in the IPv4 datagram

1. Version number
   - IP protocal version of the datagram.
   - different versions of IP use different datagram formats.
   
2. Header Length
   - IPv4 datagram contain a variable number of options,
   - are needed to determine where the payload begins
   - most IP datagram do not contain options, so typical IP datagram has a 20 bytes header.
   
3. Type Of Service (TOS)
   - allow different types of IP datagrams to be distinguished from each other.
   - e.g. real-time datagrams and non-real-time datagrams
   - two of the TOS bits are used for Explict Congestion Notification.

4. Datagram Length
   - the total length of the IP datagram (header plus data)
   - 16-bits, the theoretical maximum size of the IP datagram is 65,535 bytes. 
   - datagrams are rarely larger than 1,500 bytes, which alow to fit the maxmally payload sized Ethernet frame.

5. Identifier, flags, fragmentation offset.
   - the three fields have to do with IP fragmentation.
     - a large IP datagram is broken into serveral smaller IP datagrams
     - IPv6 does not allow IP fragmentation.

6. Time-to-live (TTL)
   - the TTL field is included to ensure that datagrams do not circulat forever (a long-lived routing loop)
   - this field decrement each time the datagram is processed by a router
   - if TTL reaches 0, a router must drop that datagram
   
7. Upper-layer protocal field
   - used when an IP datagram reaches its final destination
   - indicates the specific transport-layer protocal to which the data protion of this IP datagram should be passed
   - value 6 indicates TCP
   - value 17 indicates UDP
   - protocal number is the glue that binds the network and transport layer together.
   - the port number is the glue that binds the transport and applicaton layers together.
