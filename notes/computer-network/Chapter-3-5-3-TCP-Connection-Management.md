### learning TCP connection management is important?
1. TCP connetion establishment can significantly add to perceived delays.
2. futhermore, many common network attacks such as SYN flood attack, which exploit vulnerablities in TCP connection management.

### how a TCP connetion is established?

1. SYN segment
   the client-side TCP first sends a special TCP segment to the server-side TCP - SYN segment.
   - SYN segment
   1. no application-layer data
   2. SYN flag bit = 1
   3. randomly chooses an initial sequence number (client_isn) in sequence number field
   then the SYN segment is encapsulated within an IP datagram and send to the server.
   
   > the randomly choose the cliend_isn could avoid certain security attacks

2. SYNACK segment
   once the segment arrives at the server host
   1. the server extracts the TCP SYN segment, allocates the TCP buffers and variables to the connection
   2. sends SYNACK segment to the client
   - SYNACK segment
   1. no application-layer data
   2. SYN flag bit = 1
   3. randomly chooses its own sequence number `service_isn`
   4. acknowledgment fiels = `client_isn` + 1

3. last stage of three-way handshake
   1. Upon receiving the SYNACK segment, the client also allocates buffer and variables to the connection.
   2. send last segment of three-way handshake
   - last segment
   1. acknowledgment field = `service_isn` + 1
   2. SYN field = 0, because the connection is established
   3. could carry client-to-service data in the segment payload.
   
> three-way handshake just like a rock climber and a belayer, ensure both sides are ready.

### End of TCP connetion

support client wants to close the connection.
1. client send a FIN segment to the server
   - FIN segment
     FIN flag bit = 1
2. the server send an acknowledgment segment in return 
3. when server's running job are finished
   the server sends its own shutdown segment that FIN = 1
4. the client acknowledges the server's shutdown segment
5. at this point, all resources in the two hosts are now deallocated.(after the Time-Wait state, which is CLOSED state)

### TCP states
#### client TCP states
1. CLOSED
2. SYN_SENT
   after send the SYN segment, the client TCP enters SYN_SENT state, waiting for SYNACK segment
3. ESTABLISHED
   after receive the SYNACK segment from server, the client TCP enters ESTABLISHED state.
   while in the ESTABLISHED state, the TCP client can send and receive TCP segments containing payload.
4. FIN_WAIT_1
   after the client send FIN segment, it enters FIN_WAIT_1 state, waiting for a acknowledgment for this FIN segment
5. FIN_WAIT_2
   after receive an ACK segment for the first FIN segment, the client enters FIN_WAIT_2 state
   the client waits for another FIN segment from server
6. TIME_WAIT
   after receive the FIN segment from server, the client send a ACK segment back, and enters TIME_WAIT state.
   after time wait, the connection formally closed, all resources including the port number on the client side all all closed.
   > why need time wait?
   > because the last ACK from client-to-server may be lost and corrupt, in which case, the client need retranmissted the ACK, enable the server could successfuly deallocated the resources
   - the time spend in the TIME_WAIT state is implementation-dependent, typical values are 30 seconds, 1 minute, 2 minute.

#### the server side TCP states
> assuming the client begins connection teardown, only shown how a TCP connection is normally established and shut down
> We have not described what hap- pens in certain pathological scenarios, for example, when both sides of a connection want to initiate or shut down at the same time.

1. CLOSED
   receive last ACK.
2. LISTEN
   server application creates a listen socket
3. SYN_RCVD
   Receive SYN
   send SYN & ACK
4. ESTABLISHED
   Receive ACK
5. CLOSE_WAIT
   Receive FIN
   send ACK
6. LAST_ACK
   send FIN
   
#### when host receive a TCP segment whost port number or source IP address do not match with any of the ongoing sockets in the host
the host send a special reset segment has `RST` flag = 1, told the client do not resend the segment.

#### when a host receives a UDP packet whose destination port number not match with an ongoing UDP socket.
the host send a special ICMP datagram.

### nmap
> nmap is a port-scanning tool
> nmap can 'case the joint' not only for open TCP ports, but also for open UDP ports, for firewalls and their configurations
> even for the versions of applications and operating systems.

suppose nmap want to explore a TCP port 6789
1. nmap send a TCP SYN segment with desitination port 6789 to that host
   1. the source host receive a TCP SYNACK segment from the target host
      means the TCP port 6789 is running on the target host
   2. the source host receives a TCP RST segment from the target host
      means the target host is not running an application with TCP port 6789
      > but the attaker at least knows that the segments destined to the host at port 6789 are not blocked by an firewall on the path between source and target hosuts
   3. the source host receives nothing.
      likely means the SYN segment was bloked by an intervening firwall and never reached the target host.
      
### The SYN FLOOD Attack      

> a server allocates and initializes connection varaibles and buffers in response to receive SYN.

> the server then sends a SYNACK in response, awaits an ACK segment from the client.
> if the client dose not send an ACK to completed the third step of three-way handshake,
> eventually(after a minute or more) the server will terminate the half-open connection and reclaim the allocated resouces.

#### Dos attack also known as the SYN Flood Attack
- the attacker(s) send a large number of TCP SYN segments, without completing the third handshake step.
  the server's connection resources become exhausted as they allocated for half-open connections.
  and legitimate clients are then denied service.
  
- SYN cookies
> an effective defense are deployed in most major operating systems.

1. when the server receives a SYN segment, instead of creating a half-open connection for this SYN, 
   the server creates an initial TCP sequence number that is a complicated function(hash function) of source and
   destination IP addresses and port numbers of the SYN segment, **as well as a secret number only known to the server**
   > this carefully crafted inital sequence number is the so-called "cookie"
   
2. the server then sends the client a SYNACK packet with this special sequence number.
   > Importantly, the server does not remember the cookie or any other state information corresponding to the SYN.

3. Legitimate client will return an ACK segment with this special sequence number + 1
   > The server use the hash function could compute the right acknowledgment field value

