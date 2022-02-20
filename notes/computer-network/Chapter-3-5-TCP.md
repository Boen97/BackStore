## Connection-Oriented Transport: TCP

The TCP connection are a logical connection, with common state only in the TCPs in the two communicating end sytems
the intermediate network do not main TCP connection states. they see datagrams not connections.

- TCP connection are a full-duplex service
  flow could from A to B, at the same time, from B to A

- multicasting not possible in TCP
  multicasting: transfer of data from one sender to many receivers in a single send operations.
  there is only you and I, no three.
  
- send buffer
  which is one of buffers that is set aside during the initial three-way handshake

- MSS (maximum segment size)
  the maximum amount of **data** that can be grabbled and placed in a segment
  not the maximum size of segment

- MTU (maximum transimission unit)
  largest link-layer frame
  - MSS is typically set by MTU
  - TCP/IP header length is typically 40 bytes
  - Both Ethernet and PPP link-layer protocal have an MTU of 1500 bytes
  - so a typical of MSS is 1500 - 40 = 1460 bytes
 
 - recever's buffer
   application read the stream of data from this buffer
   
### TCP Segment Structure



