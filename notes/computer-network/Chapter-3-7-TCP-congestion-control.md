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






