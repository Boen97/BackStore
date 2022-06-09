# Message Integrity and Digital Signatures.

- `message integrity` also known as `message authentication`
- along with `message integrity`, two related topics: `digital signatures` and `end-point authentication`

> to authenticate a message, two things needs to verify
1. The message indeed originated from Alice.
2. The message was not tampered with on its way to Bob.

## Cryptographic Hash Functions.

- a hash function takes an input `m`, and computes a `fixed-size` string `H(m)` knowns as a `hash`.
- the `Internet checksum` and `CRCs` meet this definition.

> a `cryptographic hash function` is required to have the following additional property.
- it is computationally infeasible to find any two different message x and y such that `H(x) = H(y)`
: Informally, this property means that it is computationally infeasible for an intruder 
: to substitute one message for another message that is protected by the hash function

### MD5

- the `MD5` hash algorithm of `Ron Rivest` is in wide use today.
- it computes a `128-bit hash` in a `four-step` process consisting of a
- `padding step` (adding a one followed by enough zeros so that the length of the message if fixed)
- `append step` (appending a `64-bit` representation of the message length before padding)
- an initialization of an accumulator
- and a final looping step in which the message's 16-word blocks are processed in four rounds.

### SHA-1

- The second major hash algorithm in use today is the Secure Hash Algorithm (`SHA-1`)
- This algorithm is based on principles similar to those used in the design of `MD4`, the predecessor to `MD5`
- SHA-1, a US federal standard, is required for use whenever a cryptographic hash algorithm is needed for federal applications.
- It produces a 160-bit message digest. The longer output length makes SHA-1 more secure.
