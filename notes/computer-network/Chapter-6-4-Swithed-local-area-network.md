- link layer switches operate at link layer, switch link-layer frames, do not recognize network-layer addresses
> link layer switches use **link-layer addresses** to forward link-layer frames through the network of switches

## 6.4.1 Link-Layer Addressing and ARP

- ARP (Address Resolution Protocol)
: provides a mechanism to translate IP addresses to link-layer addresses

> why do we need have address at both the network and link layer?

### MAC Addresses or LAN Addresses or Physical Addesses

> it is not hosts and routers that have link-layer addresses but rather their adapters (network interfaces) that have link-layer addresses

> the link-layer switches do not have link-layer addresses associated with their interfaces that connect to hosts and routers.
> **the job of link-layer switch is to carray datagrams between hosts and routers**
> a switch does this carray transparently
> the host and router does not need to explicitly address the frame to the intervening switch

- for most LANs (including Ethernet and 802.11 wireless LANs), the MAC address is 6 bytes long

> although MAC addresses were designed to be permanent, it is possible to change an adapter's MAC address via software
