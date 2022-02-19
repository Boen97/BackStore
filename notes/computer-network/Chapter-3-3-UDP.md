 - Why UDP?
 if you want pass the transport layer and directly communicate with the network layer
 then you need a no-frills, bare-bones transport protocal, which provide the basic multiplexing and demultiplexing services
 
- The Services provided by UDP
 1. multiplexing and demultiplexing
 2. light error checking
 
- UDP Features
 
1. Finer application-level control over what data is send and when

because TCP has multi control functions, such as congestion-control, which are a little out of control by application,
if application wants more control, then UDP is a better choise

2. no connection establishment

TCP need three-way handshake to establishment connection, which are much slow then UDP

3. no connection state

TCP need maintain connection state and track parameters, such as receive and send buffer, congestion-control parameters

4. small packet header overhead

TCP segament has 20 bytes of header overhead
UDP only 8 bytes of overhead

QUIC (Quick UDP Internet Connection) which use UDP as underlying transport layer, but implements reliability in applicaion layer

- HTTP/2 runs over TCP
- HTTP/3 runs over UDP, providing error control and congestion control at the application layer
- UDP is better in Network Management, because it need to run in a stressed network state.
- when packet loss are low, and some organizations bloking UDP traffic for security reasons, 
  TCP becomes more and more popular.
- because UDP has no congestion control, which are bad for network enviroment, and will crowding out TCP sessions.
