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

- TCP segment consists of header fields and a data fields
  - header fields typically 20 bytes, 12 bytes more then the UDP header
  - data fields are chunk of size MSS, except the last chunk, which is often less then MSS
  - Interative applicatins such as remote login applications such ad ssh, chunks are often small than MSS
    segment send by ssh may be only 21 bytes

- header fields
  1. 16-bit source port
  2. 16-bit Dest port
  3. 32-bit sequence number
  4. 32-bit acknowledgment number
  5. 6-bit flag fields
     1. ACK field
     2. RST, SYN, FIN flag are used for connection setup or teardown
     3. CWR and ECE bits
        explicit congestion notification
     4. PSH 
        indicate the recever should pass the data to the upper layer immediately
     5. URG
        indicate there is data in this segament that the sending-side upper layer entity has marked as urgent
        Urgent data field
        the location of last byte of this urgent data
     (PSH, URG, Urgent data field are not used)

- sequence numbers and acknowledgment numbers
  
  - sequence number
    
    1. TCP views data as an ordered, stream of bytes, and the sequence number is a byte stream number
       for example, a data of stream are 50000 bytes, MSS are 1000 bytes
       the first segment sequence number are 0
       the second are 1000
       the third are 2000 ...
    
   - acknowledgment numbers
     the acknowledgment number that Host A puts in its segament is the sequence number of the next byte Host is expecting from Host B
 
- TCP provides cumulative acknowledgment   
   TCP only acknowledgment bytes up to first missing byte in the stream

- What does a host do when it received out-of-order segaments in a TCP connection?
> TCP RFCs do not impose any rules about this, and leave it to the progammers
1. immediately discard the out-of-order segaments
2. keep the out-of-order bytes and waits for the missing bytes to fill in the gap.
   this is the approach taken in practice


    
     


