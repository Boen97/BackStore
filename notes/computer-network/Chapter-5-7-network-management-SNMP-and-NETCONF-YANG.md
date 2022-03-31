## Network Management and SNMP, NETCONF/YANG

### the network management framework

#### key components of network management

> 1. Managing server.
   : the managing server is an application.
   : typically with network managers in the loop.
   : running in NOC (network operation center).
   : the managing server is the locus of activity for network management
   : it controls the collection, processing, analysis, and dispatching of network management information and commands.
   : it is here that actions are inited to configure, monitor, and control the network's devices.
   
> 2. Managed device.
   : a managed device might be a host, router, switch, middlebox, modem, or other network connected device.
   
> 3. Data.
    : each managed device will have data, also known as state.
    - **configuration data**
    : device information explicitly configured by the network manager.
    : such as IP address of interface speed for a device interface.
    - **operational data**
    : information that device acquires as it operates
    - **device statistics**
    : status indicators and counts metrics
    
> 4. Network management agent.
    : the network management agent is a software process running in the managed device
    : that communicates with the managing server
    : take local actions at the managed device under the command and control of the managing server.

> 5. Network management protocol.
    : this protocol runs between the managing server and the managed devices
    : allowing the managing server to query the status of managed devices
    : and take actions at these devices via its agents.

#### Three ways to manage the network

> 1. CLI (Command Line Interface)
    : CLI use is prone to errors
    : and it is difficult to automate or efficiently scale for large networks.

> 2. SNMP/MIB
    : **Management Information Base(MIB)**
    : the operator can query/set the data contained in a device's MIB objects using the **SNMP**, **Simple Network Management Protocol**
    : typically, operator use this approach to query and monitor operational state and device statistics
    : and then use CLI to actively control/configure the device.
    : it is a approach manage devices individually.
    : it has shortcoming for device configuration and network management at scale.
    : **This gave rise to the most recent approach, using NETCONF and YANG**

> 3. NETCONF/YANG
    : the NETCONF/YANG is more abstract
    : provide holistic view toward network management
    : much stronger emphasis on configuration management.
    : including specifying correctness constraints
    : providing atomic management operations over multiple controlled devices.
    > YNAG is a data modeling language used to model configuration and operational data.
    > The NETCONF protocol is used to communicate YANG-compatible actions and data to/from/among remote devices.
