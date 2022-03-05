## Generalized-forwaring-and-SDN

- destination-based forwarding
  1. match 
  2. action
  
- generalized match-plus-action capabilites are implemented via a remote controller that computes, installs, and updates these tables.

- Open Flow
  > our fllowing discussion of generalized forwarding will be based on Open Flow.
  
- Flow table
  - match-plus-action forwarding table known as flow table in OpenFlow.
    - each entry in the flow table includes:
    1. a set of header field values
       - to which an incoming packet will be matched.
       - a packet that matched no flow table entry can be dropped or sent to the remote controller for more processing.
       
    2. a set of counters.
       - are updated as packets are matched to flow table entries.
       - include the number of packets that have been macthed by that table entry.
       - the time since the table entry was last updated.
       
    3. a set of actions to be taken.
       - when a packet matches a flow table entry, these actions might be:
       1. forwardt the packet to a given ouput port
       2. drop the packet
       3. makes copies of the packet, and send them to multiple output ports
       4. rewrite selected header fields.
    
- Open Flow - generalized forwarding can do 
> use flow table entry. 
1. load balancing
2. firewall
3. virtual networks
   - two or more logically separate networks - that use the same physical set of packet switches and links.
4. programmability
   - custom match-plus-action flow tables show a limited form of programmability.
   - or use a programming language with higher-level features for datagram processing at line rate.
