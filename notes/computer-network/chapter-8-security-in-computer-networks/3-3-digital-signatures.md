# Digital Signatures

- just like you signed your name to a piece of paper.
- your signature attests to the fact that you have acknownledged with the document's content.

> in a digital world, one often wants to indicate the `owner or creator` of a document.
> or to signify one's agreement with a document's content.

> a `digital signature` is a `cryptographic technique` for this goal in a digital world.

- just as with handwritten signatures, `digital signing` should be done in a way that is `verifiable` and `nonforgeable`

- public-key cryptography is an excellent candidate for providing digital signatures. 

- One concern with signing data by encryption is that encryption and decryption are `computationally expensive`
- given the overheads of encryption and decryption, signing data via `complete encryption/decryption can be overkill`
> a more efficient approach is to introduce `hash functions` into `digital signature`
> using a `hash function`, Bob signs the `hash of the message` rather than the message itself.

## compare MAC(message authentication code) with Digital Signatures

1. to create a `MAC`, we append an `authentication key` to the message, and then takes the `hash of the result.`
2. neither publick key nor symmetric key encryption is involved in createing the MAC.

- digital signatures first take the hash of the message and then encrypte the message with our `private key`
- digital signatures is a `heavier` technique, since it requires an underlying `PKI` (public key infrastructure)
- `PGP` a popular secure e-mail system-use `digital signatures` for message integrity
