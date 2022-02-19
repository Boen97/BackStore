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

## reliable data transfer over a lossy channel with bit errors: rdt3.0

how to detect packet loss and what to do when packet loss occurs.

sender judiciously choose a time value such that packet loss, when times out just retransmit.

rdt3.0 also called alternating-bit protocol because packet sequence number alternate between 0 and 1.
       