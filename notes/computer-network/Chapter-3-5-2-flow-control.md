### why need Flow Control in TCP connection.

- each side of a TCP connection set aside a receive buffer for the connection, the associated application will read data from this buffer, but may not in time
- if the application is slow reading the data in the buffer, the buffer is very easy to overflow by sending to much data.
- so we need flow control in TCP.

- TCP provide flow-control service to its applications to eliminate the possiblity of the sender overflowing the receiver's buffer.

- Flow control is speed matching service
  match the speed of send and receive
  
- Flow control and Congestion control are very similar, both throttling the sender, but they are taken for very difference reason.


