## where does queuing occur

> packets queues may form at both the input ports and the output ports
> cars may wait at the inputs and outputs of the traffic intersection in our roundabout analogy

- the queuing depends on the traffic load, the switching fabric, the line speed
- when buffers are full, then packet loss will occur.

### Input Queuing

> the switch fabric is not fase enough (relative to the input lien speed)

- if two packets at the front of queues are destined for the same output queue
- then one of packets must wait at the input queue
- the switching fabric can transfer only one packet to a given output port at a time.
- HOL blocking (head-of-the-line blocking) in input queue
  - a queued packet in an input queue must wait for transfer throught the fabric, because it is blocked by another packet at the head of line.


