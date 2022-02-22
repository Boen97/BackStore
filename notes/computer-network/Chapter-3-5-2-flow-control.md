### why need Flow Control in TCP connection.

- each side of a TCP connection set aside a receive buffer for the connection, the associated application will read data from this buffer, but may not in time
- if the application is slow reading the data in the buffer, the buffer is very easy to overflow by sending to much data.
- so we need flow control in TCP.

- TCP provide flow-control service to its applications to eliminate the possiblity of the sender overflowing the receiver's buffer.

- Flow control is speed matching service
  match the speed of send and receive
  
- Flow control and Congestion control are very similar, both throttling the sender, but they are taken for very difference reason.

### receive window

- TCP provides flow control by having the sender maintain  a variable called the receive window.

- the receive window is to give the sender an idea of how much free space is available at the receiver.

- TCP is full-duplex, the sender at each side of the connection maintains a distinct receive window.

- suppose the size of receive buffer is RcvBuffer, from time to time, the application reads from the buffer.

- LastByteRead
  the number of last byte in the data stream read from the buffer by the application process.

- LastByteRcvd
  the number of last byte in the data stream that has arrived from the network and has been placed in the receive buffer.
  
- TCP is not permitted to overflow the allocated buffer. we must have
  `LastByteRcvd - LastByteRead <= RcvBuffer`
  
- The receive window: `rwnd` is set to the amount spare room in the buffer.
  `rwnd = RcvBuffer - (LastByteRcvd - LastByteRead)`

#### how does the connection use the variable rwnd to provide the flow-control service?

> suppose Host A is sending data to Host B

1. Host B put `rnwd` in the receive window field of every segment

2. Initially, `rnwd = RcvBuffer`

3. Host the sender, keep track of `LastByteSend`, `LastByteAcked`

4. `LastByteSend - LastByteAcked`
   is the amount of unacknowledged data that the sender has send into the connection
   
5. `LastByteSend - LastByteAcked <= rnwd`
   By keeping the amount of unacknowledged data less than the value of `rnwd`, the sender is assured that it is not overflowing the receive buffer at Host B
   
6. minor technical problem 
   1. suppose HostB's receive buffer becomes full so that `rnwd = 0`
   2. as the application process at B empties the buffer, TCP dose not send new segment with new rnwd values to Host A
   3. TCP sends a segment to Host A only if it has data to send or if it has an acknowledgment to send.
   4. to solve this problem, the TCP sepecifications requires Host A to continue to send segments with one data byte when B'receive window is zero.

- UDP does not provide flow control and consequently segments may be lost at the receiver due to overflow.



