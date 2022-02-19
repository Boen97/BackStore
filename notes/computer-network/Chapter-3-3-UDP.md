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

### UDP Segment Structure

four fields + application data
1. four fields
   1. Source Port
   2. Desc.Port
   3. Length (header + data)
      every UDP segament could have different size
   4. Checksum
      used by the receiving host to check whether has errors during the transfer
      
every field are 16 bits long

2. application data

### UDP Checksum
> provides for error detection. determine whether bits within the UDP segament have been altered.

1. get the sum of the top three 16-bits field
2. 1s complement the sum
3. at the receiver, get the sum of the four field, include the checksum field
4. if no error, then the sum in the receiver are 111111111111, if has one 0, then the segament has error

- why UDP provide checksum service, because lower link protocal also provide error checking?

end-to-end principle, certain functions must be implemented on the end, lower levels may be redundant.

there is no promise that lower service would provide errro checking

- UDP provides error checking, but does nothing to recover from an error.

- some implentations of UDP may discard the damaged segament, others pass to the application with a warning