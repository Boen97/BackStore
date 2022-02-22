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
   
