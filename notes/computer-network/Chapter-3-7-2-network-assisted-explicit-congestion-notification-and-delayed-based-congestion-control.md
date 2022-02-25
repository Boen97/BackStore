### Network-Assisted Explicit Congestion Notification and Delayed-based Congestion Control.

#### Explicit Congestion Notification (ECN)
> two bits in the Type of Service field of the IP datagram header are used for ECN
1. when router detects congestion, the router setting the ECN bits for this datagram, and sending this to the receiver
2. the receiver receipt this datagram with congestion notification ECN bits, setting ECE bits in the segment, then send it to the sender
3. the sender receive this ACk, and react to this congestion notification, such as halving the congestion window.
> a congested router can set the congestion indication bit to signal congestion onset to senders before full buffers cause packets to be dropped at that router.
#### Delayed-based Congestion Control
> measure the RTT of the source-to-destination path for all acknowledged packets.
- RTTmin is the minimum of these measurements at a sender.
- the uncongestd throughput rate would be cwnd/RTTmin
- if the actual sender-measured throughput is close to this value, then increase the sending rate
- if the actual sender-measured throughput is signifi- cantly less than the uncongested throughput rate, the path is congested and decrease its sending rate
- The BBR congestion control protocol build on the this idea.

> The BBR congestion control protocol [Cardwell 2017] builds on ideas in TCP Vegas, and incorporates mechanisms that allows it compete fairly (see Section 3.7.3) with TCP non-BBR senders

> Google began using BBR for all TCP traffic on its private B4 network [Jain 2013] that intercon- nects Google data centers, replacing CUBIC.

#### Fairness

> consider K TCP connections, each with a different end-to-end path, but all passing through a bottleneck link with transmission rate R bps.

- if congestion control is said to be fair
  - average transmission rate of each connection is R/K, each connection gets an equal share of link bandwidth.
  
- Is TCP's AIMD algorithm fair, particularly given that different TCP connec- tions may start at different times and thus may have different window sizes at a given point in time?

- multiple connections share a common bottleneck, those sessions with a smaller RTT are able to grab the available bandwidth at that link more quickly as it becomes free (that is, open their congestion windows faster) and thus will enjoy higher throughput than those connections with larger RTTs 

##### Fairness and UDP
the multimedia applications running over UDP are not being fair—they do not cooperate with the other connections nor adjust their transmission rates appropriately. Because TCP congestion control will decrease its transmission rate in the face of increasing congestion (loss)

##### Fairness and Parallel TCP Connections

there is nothing to stop a TCP-based application from using multiple parallel connections. 

When an application uses multiple parallel connections, it gets a larger fraction of the bandwidth in a congested link.
