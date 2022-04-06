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

#### Checksumming Methods
> in checksumming methods, the d bits of data are treated as a sequence of k-bit integers.
- the Internet checksum
  : bytes of data are treated as 16-bit integers and summed.
  : the 1s complement of this sum then forms the Internet checksum that is carried in the segment header.
- checksumming methods require relatively little packet overhead.
  : the checksums in TCP and UDP use only 16 bits
  
> why is checksumming used at the transport layer and cyclic redundancy check used at the link layer?
: transport layer is typically implemented in software in a host as part of host's operating system.
: Because transport-layer error detection is implemented in software, it is important to have a simple and fast error-detection scheme such as checksumming. 
: error detection at the link layer is implemented in dedicated hardware in adapters

#### Cyclic Redundancy Check (CRC)
- **CRC codes (Cyclic Redundancy Check) codes**
: widely used in today's computer network

- **CRC codes** also known as **polynomial codes**
: since it is possible to view the bit string to be sent as a polynomial whose coefficients are the 0 and 1 value in the bit string.
: with operations on the bit string interpreted as polynomial arithmetic.

> The sender and receiver must first agree on an **r + 1** bit pattern, known as a **generator**, which we will denote as **G**.
> the most significat (leftmost) bit of G is 1.
> for a given piece of data, D, the sender will choosed **r additional bits R**, and append them to D
> **such that the resulting d + r bit pattern is exactly divisible by G** using modulo-2 arithmetic

> The receiver divides the d + r received bits by G
> If the reminder is nonzero, the receiver knowns that an error has occurred.
> otherwise the data is accepted as being correct.
