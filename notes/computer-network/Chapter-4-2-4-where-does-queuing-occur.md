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

### Output Queuing

- when output buffers are full
  1. drop-tail
  2. remove one or more already-queued packets
- provide a congesion signal to the sender before the buffer is full
  1. drop a packet
  2. mark the header of packet
     1. Explict Congestion Notification
     2. AQM (Active Queue management) algorithms
        - a number of proactive packet-dropping and marking policies
        - RED (Random Earyly Detection) algorithm
          - most widely studied and implimented AQM algorith

### How much space is enough?
- rule of thumb for buffer sizing
  - B the amount of buffering 
  - RTT round-trip-time
  - C the link capacity
  - B = RTT * C
  - a 10-Gbps link with RTT(250msec) B = 2.5Gbps
  > based on small number of TCP flows

- with a large number of TCP flows (N)
  - N the large number of TCP flows
  - B = RTT * C / square of N
  
- Buffering is a double edged sword
  > Buffering is like a salt, just the right amount of salt makes food better, but too much makes it inedible
  - larger buffers have problems describe below:
    1. longer queuing delays
       -  Increasing the amount of per-hop buffer by a factor of 10 to decrease packet loss could increase the end-end delay by a factor of 10
    2. increased RTTs make TCP sender less responsive and slower to response to congestion and packet loss
