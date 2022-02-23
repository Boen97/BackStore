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

> Bandwidth probing
Given ACKs indicating a congestion-free source-to-destination path and loss events indicating a congested path.
- loss evensts
  1. timeout
  2. an original ACK and then three duplicate ACKs
> The TCP sender's behaviour is like a child who requets (and gets) more and more goodies until finally he is finally told no.
> but then begins making request again shortly afterward.

- ACKs and loss events serve as implicit signals

- each TCP sender acts on local information asynchronously from other TCP senders.

#### TCP congestion-control algorithm

- three major components
1. slow start
2. congestion avoidence
3. fast recovery (recommend, not required)

##### slow start
1. `cwnd` is initialized to a small value of 1 MSS(maximum segment size)
2. increase by 1 MSS every time a transimitted segment is first acknowledged
   - first 1 MSS
   - then 2 MSS
   - then 4 MSS
   - starts slow but grows exponentially
3. when a loss event indicated by a timeout
   - set the value of `cwnd` to 1 and begins the slow start anew
   - aslo set the `ssthresh`(shorthand for (slow start threshold)) to `cwnd / 2`
4. since `ssthresh` is half the value of `cwnd` when congestion was last detected, it might be a bit reckless to keep 
   doubling `cwnd` when it reaches or surpasses the value of `ssthresh`
5. thus when `cwn` equals `ssthresh`, slow start ends and TCP transitions into **congestion avoidence mode**
6. if three duplicate ACKs are detected, TCP performs fast retransmit, and enters the fast recovery state.


   





