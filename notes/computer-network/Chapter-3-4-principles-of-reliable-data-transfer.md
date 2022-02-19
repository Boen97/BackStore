> consider the problem of reliable data transfer in a general context.

the problem of reliable data transfer occurs not only at the transport layer, but also at the link layer and the application layer as well.

and the problem of reliable data transfer is top-ten list of important problems in all networking.

- reliable channel

with a reliable channel, no transferred data bits are corrupted or lost, and all are delivered in the order which they were sent

## build a reliable data transfer protocol.

### reliable data transfer over a perfectly reliable channel: rdt1.0

- FSM (Finite-state-machine)
1. dashed arrow are initial state of the FSM
2. above the horizontal line are the event causing the state tansition
3. below the horizontal line are the actions taken when the event occurs

- rdt1.0 no need any feedback from the receiver side
- rdt1.0 are assumed that receiver is able to receive data as fast as possible, so there is no need to ask the sender to slow down.

### reliable data transfer over a channel with bit errors: rdt2.0

with bit errors but no packet loss

- feeback

feedback are needed when receive a bit error packet
1. positive acknowledgments
2. negative acknowledgments

- ARQ protocals (Automatic Repeat reQuest) 
1. error detection
2. receiver feedback
3. retransmission

- stop-and-wait protol
  - the sender has two states, one wait call from above, one wait for ACK or NAK
  - the receiver has one state, wait for call from below
  - when the sender in the wait-for-ACK-or-NAK state, it cannot get more data from the upper layer

- fatal flaw of rdt2.0
  - the ACK or NAK packet could be corrupted

- solve the corrupted ACK or NAK packet
  - first, we need add checksum to detect errors
  - ways for handle corrupted ACKs or NAKs
    1. add a new type of packect, "what did you say"
    2. add enough checksum bits allow the sender not only to detect, but also to recover from bit errors.
       in rdt2.0 no packect loss, so it would work
    3. resend
       when sender receiver garbled ACK or NAK.
       This brings a new problem: duplicate packets

### rdt2.1 add sequence number field

based on rdt2.0, with sequence number, we could clearly reslove the duplicate packets problem

### rdt2.2 NAK-free 

based on rdt2.1, instead respones NAK, send an ACK for the last corretly received packet

### reliable data transfer over a lossy channel with bit errors: rdt3.0

how to detect packet loss and what to do when packet loss occurs.

sender judiciously choose a time value such that packet loss, when times out just retransmit.

rdt3.0 also called alternating-bit protocol because packet sequence number alternate between 0 and 1.
       
### pipelined reliable data transfer protocals

rdt3.0 has bad performance because its stop-and-wait protocal.
the wait time are slow down the transimit rate.

the sender is allowed to transmit multiple packets without waiting for ACK

1. the range of sequence number increased
2. both side have to buffer more than one packet
3. new approaches are need to error recover with a range of sequence number
   1. Go-Back-N
   2. selective repeat
   
#### Go-Back-N(GBN) also called sliding-window protocal

maximun allowed number N, of unacknowledged packtes in the pipeline

just like a send window size N

- base 
  the sequence number of the oldest unacknowledged packet

- nextseqnum
  smallest unused sequence number
  
- [0 - base - 1]
  packets that have been acknowledged
  
- [base - nextseqnum - 1]
  packect that have been sent but not yes acknowledged
  
- [nextseqnum - base + N - 1]
  can be used for packects send immediately

- [base + N - ...]
  cannot be used 

- k
  is the number of bits in the packet sequence number field
  so its a ring of size z^k

- TCP has a 32-bit sequence number field

- The GBN sender respond events

1. Invocation from above
   
   if the window is not full, then a packet will be send
   otherwise put it to a buffer or use a semaphore or a flag to control the access of send window
   
2. Receipt of ACK
   - cumulative acknowledgment
     all packects with a sequence number up to and include n have been corretly received.

3. a timeout event
   a timer for the oldest transmitted but not yet acknowledged
   when a ACK received
   1. there still additional wait ACK packets, then timer restarted
   2. no other waiting, then stopped.
  



#### Selective Repeat(SR)