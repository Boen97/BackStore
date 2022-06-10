# The big Picture

> get a big-picture understanding of the `why and how of TLS`

- simplified version of `TLS` as `almost-TLS`

> Almost-TLS has three phases: `handshake, key derivation and data transfer`

## example

- example between a `client(Bob)` and a `server(Alice)`
- Alice having a `private/public key` pair and a `certificate` that binds her identity to her public key.

## Handshake

- during the handshake phase, Bob needs to:
1. establish a TCP connection with Alice
2. verify that Alice is really Alice
3. send Alice a `master secret key`
