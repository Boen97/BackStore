## SDN Controller and SDN Network-control Applications

> a Controller's functionality can be broadly organized into three layers.

1. **A communication Layer***
   : communicating between the SDN controller and controlled network devices
   : a protocol is needed to transfer information between the controller and the devices.
   : a device must be able to communicate locally-observed events to the controller.
   : OpenFlow is a specify protocol that provides this communication functionality 
2. **A network-wide state-management layer**
   : the controller have up-to-date information about the state of the network's hosts, links, switches, and other SDN-controlled devices.
   : the ultimate control decisions made by the SDN control plane
3. **the interface to the network-control**
