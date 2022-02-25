### Evolution of transport layer functionality

> three decades of experience with these two protocols has identified circumstances in which neither is ideally suited, and so the design and implementation of transport layer functionality has continued to evolve.

#### QUIC (Quick UDP Internet Connections)

> QUIC is a new application-layer protocol designed from the ground up to improve the performance of transport-layer services for secure HTTP.
> QUIC is an application-layer protocol, using UDP as its underlying transport-layer protocol, and is designed to interface above specifi- cally to a simplified but evolved version of HTTP/2

##### QUIC features

1. Connection-Oriented and Secure
> QUIC combines the handshakes needed to establish connection state with those  needed for authentication and encryption, proving faster establishment.
> while traditional secure HTTP protocol stack need multiple RTTs are required to first establish a TCP connection, then establish a TLS connection over the TCP connection.

2. Streams

> QUIC allows several different application-level streams to be multiplexd through a single QUIC connection.
> once a QUIC connection is established, new streams can be quickly added.
- A stream is an abstraction for the reliable, in-order bi-directional delivery of data between two QUIC endpoints
- each connection has an connection ID, and each stream within a connection has a stream ID
- both of these IDs are contained in the QUIC packet header.
- Data from multiple streams may be contained within a sinle QUIC segment.
- In the context of HTTP/3, there would be a different stream for each object in a Web page.
- SCTP(The stream control transimission protocol) is an earlier reliable, message-oriented protocol that pioneered the notion of multiplexing multiple appli- cation-level “streams” through a single SCTP connection. 
- SCTP is used in control plane protocols in 4G/5G cellular wireless networks.

3. Reliable, TCP-friendly congestion-controlled data transfer.
> QUIC provides reliable data transfer to each QUIC stream separately
- the case of HTTP/1.1 sending multiple HTTP requests, all over a single TCP connection.
  - this means that the multiple HTTP requests must be delivered inorder at the destination HTTP server
  -  if bytes from one HTTP request are lost, the remaining HTTP requests can not be delivered until those lost bytes are retransmitted and correctly received by TCP at the HTTP server
  - the so-called HOL blocking problem that we encountered earlier in Section 2.2.5.
- QUIC provides a reliable in-order delivery on a per-stream basis, a lost UDP segment only impacts those streams whose data was carried in that segment;
- HTTP messages in other streams can continue to be received and delivered to the application. 

- QUIC’s congestion control is based on TCP NewReno
