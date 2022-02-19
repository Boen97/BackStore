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