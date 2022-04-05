## bit-level error detection and correction

- **EDC (error-detection and correction bits)**

- suppose D is the sending data
- the data to be protected includes not only datagram passed down from the network layer for transimission across the link.
- but also link-level addressing information, sequence number, and other fields in the link frame header.
- both D and EDC are sent to the receiving node in a link-level frame.
- in the receiving node, a sequence of bits, **D' and EDC'** is received.
- D' and EDC' may differ from the original D and EDC as a result of in-transit bit flips.

> the receiver's challenge is to determine whether or not D' is the same as the original D
> given that it has received D' and EDC'.

> error-dection and correction techniques allow the receiver to sometimes, **but not always detect that bit errors have occurred**
> **even with the use of error-dection bits there still may be undetected bit errors.**

> more error-dection and correction incurs a larger overhead.

### three techniques for detecting errors in the transmitted data
1. parity checks (the basic idea behind error dection and correction)
2. checksumming methods (typically used in the transport layer)
3. cyclic redundancy checks (typically used in the link layer in an adapter)


#### Parity Checks

> simplest form of error detection is use of a single **parity bit**

- in a even parity scheme, the sender simply includes one additional bit and choose its value such that the total number of 1s in the d + 1 bits is even.
- for odd parity schemes, the parity bit value is chosen such that there is odd number of 1s.

> the receiver need only count the number of 1s in the received d + 1 bits.
- if an odd number of 1-valued bits are found with an even parity scheme,
- the receiver knows that at least one bit error has occurred.

> **errors are often clustered together in bursts**

- **two-dimensional parity** schema
- the parity of both the column and the row containing the flipped bit will be in error.
- use the column and row indices of the column and row with parity errors to actually identify the bit and correct that error.

- **FEC (forward error correction)**
> the ability of the receiver to both detect and correct errors is known as FEC
- FEC can decrease the number of sender retransmissions required.
