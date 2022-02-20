IP service are reliable, datagrams can loss, corrupt, and out of order. transport layer suffer from this.

TCP's reliable data transfer service ensures that the data stream that a process reads out of its TCP reveiver buffer is uncorrupted, without gaps, without duplication, and in sequence. that is the byte stream is exactly the same byte stream that was sent by the sender.

### TCP timer management

TCP use only a single retransimission timer, even if there are multiple transimitted by not yet acknowledged segaments.
because timer management can require considerable overhead.

- the timer associated with the oldest not unacknowledged segament

- TCP is cumulative acknowledgments, so sequence number Y is ACK, then before Y are all ACK.


