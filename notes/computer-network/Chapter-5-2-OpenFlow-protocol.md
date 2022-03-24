## OpenFlow Protocol

- the OpenFlow protocol operates between an SDN controller and an SDN-controlled switch or device implementing the OpenFlow API
- The OpenFlow protocol operates over TCP, with a default port number of 6653

- **important messages fllowing from the controller to the controlled switches** are the following
1. Configuration
2. Modify-State
   : add/delete or modify entries in the switch's flow table and to set switch port properties
3. Read-State
   : collect statistics and counter values from the switch's flow table and ports.
4. Send-Packet
   : send a specify packet out of a specified port at the controlled switch
   : the message itself contains the packet to be sent in its payload.

- **messages flowing from controlled switch to the controller**
1. Flow-Removed
   : informs the controller that a flow table entry has been removed.
2. Port-status
   : a change in port status
3. Packet-in
   : a packet arriving at a switch port and not matching any flow table entry is send to the controller for additional processing.
   : the packet-in message is used to send such packets to the controller
