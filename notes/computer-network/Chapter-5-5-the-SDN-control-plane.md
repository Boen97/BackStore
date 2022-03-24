## Four key characteristics of an SDN architecture 
1. Flow-based forwarding
   : SDN-controlled switches can be based on any number of header field values in the transport, network, or link-layer header.
   : it is the job of the SDN control plane to compute, manage and install flow tables entries to all switches.
   
2. Separation of data plane and control plane.
   : the data plane consists of the switches, which execute the match plus action rules in theirs flow table.
   : the control plane consists of servers and software that determine and manage the switches' flow table.
   
3. Network control functions: external to data-plane switches.
   - the control plane consists of two components:
   1. an SDN controller (or network operating system)
      : the controller maintains accurate network state information
      : provides this information to the network-control applications
      : and provides means through whick these applications can monitor, program, and control the underlying network.
   2. a set of network-control applications
      : routing application
      : access control application
      : load balancer application

4. A programmable network
   : the network is programmable throught the network-control applications running in the control plane.
   : these applications represents the brains of the SDN control plane.
   : using the APIs provided by the SDN controller to specify and control the data plane in the network devices.

> SDN represents a significant unbundling of network functionality
> date plane switches, SDN controllers, and network-control applications are separate entites that may each be provided by different vendors and organizations

> this unbundling of network functionality in SDN just like the earlier evolution from mainframe computers to personal computers.
> The unbundling of computing hardware, system software, and applications has led to a rich, open ecosystem driven by innovation in all areas.
> one hope for SDN is that is will continue to drive and enable such rich innovation.
