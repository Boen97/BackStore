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

##### congestion avoidence
1. the value `cwnd` is approximately equal to `ssthresh`, the congestion is around corner
2. increase the value of `cwnd` by just a single MSS every RTT
   - the TCP sender increase `cwnd` by MSS bytes (MSS/cwnd) when every acknowledgement arrives.
     for example, if MSS is 1460 bytes and cwnd is 14600 bytes, then 10 segments are sent within an RTT
     each arriving ACK increase cwnd by MSS/cwnd (1/10) MSS
3. when timeout occurs, behave the same as slow start encounter timeout
   1. cwnd = 1
   2. ssthresh = last cwnd / 2
4. triple duplicate ACKs
   1. TCP halves the value of cwnd
   2. records the value of ssthresh to be half the value of cwnd
   3. enter fast-recovery

##### fast Recovery

In fast recovery, the value of cwnd is increased by 1 MSS for every duplicate ACK received for the missing segment that caused TCP to enter the fast-recovery state. 

when an ACK arrives for the missing segment, TCP enters the congestion-avoidence state.

when comes into fast recovery cwnd = ssthresh + 3MSS(which by fast retransmit)

#### TCP Splitting: Optimizing the performance of cloud services

> beaking the TCP connection at the front-end server which is close to user
> and the front-end maintains a persistent TCP connection to the data center with a very large TCP congestion window.
> remmber, the connection between front-end and back-end are early inited and maintained

- the client establishes a TCP connection to the nearby front-end
- the front-end server maintains a persistent TCP connection to the data center with a very large TCP congestion window
- the time without TCP Splitting
  4*RTT(one RTT to set up the connection, three for three windows of data)
- the time with TCP SPlitting
  - 4*RTT(front-end) + RTT(back-end server)
  - if the front-end server are close to client, then the front-end RTT are so small
  - and RTT(back-end server) is approximately RTT.
  > so TCP Splitting can reduce the network delay roughly from 4 * RTT to RTT
- TCP splitting also helps reduce TCP retransmission delays caused by losses in access networks.
  
   
- AIMD(additive-increase, multiplicative-decrease) congestion control 
> TCP congestion control also referred to as an AIMD form of congestion control.

#### TCP Cubic

> TCP Cubic only changes the congestion avoidence phase

- `Wmax` be the size of congestion window when loss was last detected.
- `K` be the funture point in time when TCP CUBIC' window size will again reach Wmax, **assuming no losses**
- `t` the current time
- Cubic increase the congestion window as a function of **cube of the distance between current time t and K**
  - so the time more close to K, grow more slow
  - when at the start of congestion avoidence phase, the cube of distance between t and K are large, so the congestion window will grow quickly
  - when t close to K whether or not if proceed K, the congestion window will grow slowly.
- TCP Cubic is the default version of TCP used in the linux operating system.



