# Principles of Cryptography
- the sender disguise data and the receiver recover the original data from the `disguised data`

- `plaintext` or `cleartext`
- encryption algorithm
- encrypted message, known as `ciphertext`

- the encryption techniques itself is `known-published`, standardized, and available to everyone.
- this is where `keys` come in.

- Alice use `KeyA` as input to the `encryption alogorithm`
- Bob use `KeyB` to the `decryption alogorithm` with `ciphertext` to produce the original plaintext

> in `symmetric key systems`, Alice's and Bob's keys are `identical` and are `secret`

> in `public key systems`, a pair of keys is used.
- one of the keys is known to both Bob and Alice (indeed, it is known to the whole world)
- the other key is known only by either Bob or Alice (but not both)
