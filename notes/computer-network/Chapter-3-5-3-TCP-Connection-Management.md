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
