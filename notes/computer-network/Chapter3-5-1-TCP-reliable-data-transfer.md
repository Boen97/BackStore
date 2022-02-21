IP service are reliable, datagrams can loss, corrupt, and out of order. transport layer suffer from this.

TCP's reliable data transfer service ensures that the data stream that a process reads out of its TCP reveiver buffer is uncorrupted, without gaps, without duplication, and in sequence. that is the byte stream is exactly the same byte stream that was sent by the sender.

### TCP timer management

TCP use only a single retransimission timer, even if there are multiple transimitted by not yet acknowledged segaments.
because timer management can require considerable overhead.

- the timer associated with the oldest not unacknowledged segament

- TCP is cumulative acknowledgments, so sequence number Y is ACK, then before Y are all ACK.

### Doubling the Timeout Interval

when timeout event occurs, TCP restrasimits the not-yet-acknowledged segament with the smalles sequence number.

- each time TCP retransmits, set the next timeout interval to twice as previous value.

-  when data received from application above, or ACK received, the TimeoutInterval is derived from the most recent values of EstimatedRTT and DevRTT.

- doubling the timeout interval provide a limited form of congestion control.

### Fase Retransmit

one of the problems with timeout-triggered retranmissions is that the timeout period can be relatively long.

- three duplicate ACKs are received, the TCP sender performs a fast retransmit before that segament's timer expiration.

### TCP's error-recovery mechanism is a hybrid of GBN and SR protocols.
