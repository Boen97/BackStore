- Ethernet with a bus topology is a **broadcast LAN**
- by the late 1990s, mose companies and universities replaced their LANs with Ethernet using **hub-based star topology**
- **the hosts (and routers) are directly connected to a hub with twisted-pair copper wire**

> **hub**
- a hub is a physical-layer device that acts on individual bits rather than frames
- when a bit, representing a zero or a one, arrives from one interface, the hub simply re-create the bit
- boosts its energy strength, and transmit the bit onto all the other interfaces.
- thus Ethernet with a hub-based star topology is also a broadcast LAN - whenever a hub receives a bit from one of its interfaces, it sends a copy out all of its other interfaces.

> **switch**
- In the early 2000s, Ethernet installations continued to use a star topology
- but the hub at the center was replaced with a **switch**
- a switch is not only "collision-less" but is also a **bona-fide store-and-forward packet switch.**
- **unlike routers, whick operate up through layer 3, a switch operates only up through layer 2**

## Ethernet Frame Structure
> sending adapter encapsulates the IP datagram within an Ethernet frame and passes the frame to the physical layer

1. Data field (46 to 1,500 bytes)
   : carries the IP datagram
   : **MTU** (maximum transmission unit) of Ethernet is **1,500 bytes**
   : if the IP datagram exceeds 1,500 bytes, then the host has to fragment the datagram
   : **minimum size of the data** field is **46 bytes**
   : if the IP datagram is less than 46 bytes, the data field has to be stuffed to fill it out to 46 bytes
   : the network layer uses the length field in the IP datagram header to remove the stuffing.

2. Destination address (6 bytes)
   : contains the MAC address of the desination adapter.

3. Source address (6 bytes)
   : the MAC address of the adapter that transmits the frame onto the LAN

4. Type field (2 bytes)
   : the type field permits Ethernet to multiple network-layer protocols
   : hosts can use other network-layer protocol besides IP
   
5. Cyclic redundancy check(CRC) (4 bytes)
   : allow the receving adapter, to detect bit errors in the frame

6. Preamble (8 bytes)
   : the Ethernet frame begins with an 8-byte preamble field.
   : Each of the first 7 bytes of the preamble has a value of 10101010; the last byte is 10101011. 
   : Each of the first 7 bytes of the preamble has a value of 10101010; the last byte is 10101011. 
   > Why should the clocks be out of synchronization? 
   : adapter A aims to transmit the frame at 10 Mbps, 100 Mbps, or 1 Gbps, depending on the type of Ethernet LAN.
   : However, because nothing is absolutely perfect, adapter A will not transmit the frame at exactly the target rate;
   : there will always be some **drift** from the target rate, a drift which is not known a priori by the other adapters on the LAN.
   : **A receiving adapter can lock onto adapter A’s clock simply by locking onto the bits in the first 7 bytes of the preamble.**
   : **The last 2 bits of the eighth byte of the preamble (the first two consecutive 1s) alert adapter B that the “important stuff” is about to come.**

- Ethernet provide **connectionless service** to the network layer.
  : When adapter A wants to send a datagram to adapter B
  : adapter A without first handshaking with adapter B, just directly send the frame into the LAN
  
- Ethernet provide **unreliable service** to the network layer
  : This lack of reliable transport (at the link layer) helps to make Eth- ernet simple and cheap.
  
## Ethernet Technologies


