> we can distinguish among congestion-control approaches by whether the network layer
> provides explict assistance to the transport layer for congestion-control purposes:

1. End-to-end congestion control
   1. the network layer provides no explict support
   2. the presence of network congestion must be inferred by the end systems based only on observed network behaviour(exp: packet loss and delay).
   3. TCP takes this end-to-end approach toward congestion control. because the IP layer is not required to provide feedback to host regarding network congestion.
   4. TCP segment loss (timeout or the receipt of three duplicate acknowledgments) is taken as an indication of network congestion.
   5. TCP will decrease its window size when network congestion happens
   6. a more recent proposal for TCP congestion control that use **increasing round-trip segment delay** as an indicator of increaed network congestion.

2. Network-assisted congestion control
   1. routers provides explictly feedback to the sender and/or receiver regarding the congestion state of network.
   2. a simple feedback could be a single bit indicating congestion at a link whick are used in early IBM SNA / ATM network architectures.
   3. More sophisticated feedback ATM Available Bite Rate (ABR) congestion control, a router informs the sender of the maximum host sending rate it (the router) can support on an outgoing link. 
   4.  more recently, IP and TCP may also optionally implement network-assisted congestion control.
   
   - Direct feedback
     Direct feedback may be sent from a network router to the sender. This form of notification typically takes the form of a **choke packet** (essentially say- ing, “I’m congested!”).
   - network feedback via receiver
     - more common
     - a router marks/updates a field in a packet flowing from sender to receiver to indicate congestion
     - Upon receipt of a marked packet, the receiver then notifies the sender of the congestion indication.
     - takes a full round-trip time.
     
