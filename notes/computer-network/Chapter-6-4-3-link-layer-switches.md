> The role of the switch is to receive incoming link-layer frames and forward them onto outgoing links.

## Forwarding and Filtering

1. Filtering
   : is the switch function that determines whether a frame should be for- warded to some interface or should just be dropped.

2. Forwarding
   : determines the interfaces to which a frame should be directed, and then moves the frame to those interfaces.

3. **switch table**
   : Switch filtering and forwarding are done with a switch table.
   : The switch table contains entries for some, but not necessarily all, of the hosts and routers on a LAN
   : An entry in the switch table contains
     1. a MAC address
     2. the switch interface that leads toward that MAC address
     3. the time at which the entry was placed in the table.
 
### how switch filtering and forwarding work?
> suppose a frame with destination address DD-DD-DD-DD-DD-DD arrives at the switch on interface x.
1. There is no entry in the table
   : if there is no entry for the destination address, the switch broadcasts the frame.
   
2. There is an entry in the table, associating DD-DD-DD-DD-DD-DD with interface x.
   : the switch performs the filtering function by discarding the frame.

3. There is an entry in the table, associating DD-DD-DD-DD-DD-DD with interface y != x
   : The switch performs its forwarding function by putting the frame in an output buffer that precedes interface y.

### Self learning
1. The switch table is initially empty.

2. For each incoming frame received on an interface, the switch stores
   1. the MAC address in the frame’s source address field
   2. the interface from which the frame arrived
   3. the current time. 

3. The switch deletes an address in the table if no frames are received with that address as the source address after some period of time (**the aging time**)

> Switches are plug-and-play devices because they require no intervention from a network administrator or user.
> Switches are also full-duplex, meaning any switch interface can send and receive at the same time.

### Properties of Link-Layer switching
 
1. Elimination of collisions
   : The switches buffer frames and never transmit more than one frame on a segment at any one time
   : As with a router, the maximum aggregate throughput of a switch is the sum of all the switch interface rates.
   : **switches provide a significant performance improvement over LANs with broadcast links.**

2. Heterogeneous links.
   : a switch isolates one link from another, the different links in the LAN can operate at different speeds and can run over different media.

3. Management
   : a switch also eases network management
   : if an adapter malfunctions and continually sends Ethernet frames (called a jabbering adapter
   : a switch can detect the problem and internally disconnect the malfunctioning adapter.
   : Switches also gather statistics on bandwidth usage, collision rates, and traffic types, and make this information available to the network man- ager.

### SNIFFING A SWITCHED LAN: SWITCH POISONING

- When a host is connected to a switch, it typically only receives frames that are intended for it.
- When host A sends a frame to host B, and there is an entry for host B in the switch table, 
- then the switch will forward the frame only to host B. If host C happens to be running a sniffer, host C will not be able to sniff this A-to-B frame.
- it is more difficult for an attacker to sniff frames

- **switch poisoning**
: send tons of packets to the switch with many different bogus source MAC addresses
: thereby filling the switch table with bogus entries and leaving no room for the MAC addresses of the legitimate hosts
: This causes the switch to broadcast most frames, which can then be picked up by the sniffer

### Switches Versus Routers

#### pros and cons of switches
> 1. Traffic isolation
> 2. Plug and Play

1. plug-and-play

2. have relatively high filtering and forwarding rates
   : switches have to process frames only up through layer 2, whereas routers have to process datagrams up through layer 3.

3. a large switched network would require large ARP tables in the hosts and routers and would generate substantial ARP traffic and processing.

4. switches are susceptible to broadcast storms
   : if one host goes haywire and transmits an endless stream of Ethernet broadcast frames
   : the switches will forward all of these frames, causing the entire network to collapse.

#### pros and cons of routers
> 1. traffic isolation
> 2. Optimal routing

1. Because network addressing is often hierarchical, packets do not normally cycle through routers even when the network has redundant paths

2. Thus, packets are not restricted to a spanning tree and can use the best path between source and destination

3. routers is that they provide firewall protection against layer-2 broadcast storms

4. the most significant drawback of routers
   : they are not plug-and-play
   : they and the hosts that connect to them need their IP addresses to be configured.

5. routers often have a larger per-packet processing time than switches
   : they have to process up through the layer-3 fields

#### When to use switches?

> small networks consisting of a few hundred hosts have a few LAN segments.
> Switches suffice for these small networks, as they localize traffic
> and increase aggregate throughput **without requiring any configuration of IP addresses.**

#### When to use routers?
> larger networks consisting of thousands of hosts typically include routers within the network 
> The routers provide a more robust isolation of traffic, control broadcast storms, and use more “intelligent” routes among the hosts in the network.
