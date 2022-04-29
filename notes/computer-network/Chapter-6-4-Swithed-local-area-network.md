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

> **no two adapters have the same address** because the IEEE manages the MAC address space.

> **an adapter's MAC address has a flat structure (as opposed to a hierarchical structure, such as IP address)**
> **and does not change no matter where the adapter goes**

- An adapter’s MAC address is analogous to a **person’s social security number**
- An IP address is analogous to a person’s **postal address**

> **just as a person may find it useful to have both a postal address and a social security number**
> **it is useful for a host and router interfaces to have both a network-layer address and a MAC address**

- when an adapter wants to send a frame to some destination adapter, the sending adapter inserts the destination adapter's MAC address into the frame
- a switch occasionally broadcast an incoming frame onto all of its interfaces.
- an adapter may receive an frame that isn't associated to it.
- the destination only will be interrupted when the frame is received.

> **MAC broadcast address**
- for Ethernet LANs, the MAC broadcast address was FF-FF-FF-FF-FF-FF


### ARP (Address Resolution Protocol)


