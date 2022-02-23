### Classic TCP Congestion Control

> have each sender limit the rate based a functon of perceived networdk congestion.

#### Three Questions?

1. how does a TCP sender limit the rate at which it sends traffic its connection?
2. how does a TCP sender perceived that there is congestion on the path between itself and the destination
3. what algorithms should the sender use to change its send rate as a function of perceived end-to-end congestion

> flow control more about the speed match of the sender and receiver
> whick congestion control concern more about whole network state along the path.

#### congestion window (for Q1)
> the sender keep track of the `congestion window`(`cwnd`) to operate with congestion control.

- `LastByteSent – LastByteAcked ... min{cwnd, rwnd}`
the amount of unacknowledged data at a sender may not exceed the minimum of cwnd and rnwd.

- suppose the receive buffer is so large that receive-window can be ignored

Thus the sender’s send rate is roughly cwnd/RTT bytes/sec. 
By adjusting the value of cwnd, the sender can therefore adjust the rate at which it sends data into its connection.

#### Q2 how perceived that there is congestion

> a timeout or receipt of three duplicate ACKs(fast retransmission)

#### Q3 algorithms
> if acknowledgments arrive at a relatively slow rate (e.g., if the end-end path has high delay or contains a low-bandwidth link), then the congestion window will be increased at a relatively slow rate
>  On the other hand, if acknowl- edgments arrive at a high rate, then the congestion window will be increased more quickly.

- self-clocking
> because TCP use acknowledgments to trigger(or clock) its increase in congestion window size, TCP is said to be self-clocking

- However, if TCP senders are too cautious and send too slowly, they could under utilize the bandwidth in the network; 
- that is, the TCP senders could send at a higher rate without congest- ing the network.

- algorithms
1. 





