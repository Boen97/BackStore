# End-Point Authentication

> `End-Point Authentication` is the process of one entity proving its identity
> to another entity over a `computer network`, for example, a user proving its identity to an e-mail server.

> how one party can authenticate another party when the two are communicating over a network ? 
- we focus here on `authenticating` a `live` party, at the point in time when communicating is actually occuring.
- A concrete example is a user authenticating him or herself to an e-mail server.
- this is different from proving a `received message` is indeen come from the sender.

- here, authentication must be done solely on the basis of messages and data exchanged as part of an `authentication protocol`
- an `authentication protocol` would `run before` the two communicating parties run some other protocol.

## example

1. Alice needs to authenticate herself to Bob.

### Authentication Protocol ap3.0

> use a `secret password`
- the `password` is a shared secret between the `authenticator` and the person being `authenticated`
- `Gmail, Facebook` and many other services use `password` authentication

- a `issue`
> if Trudy eavesdrops on Alice's communication, the she can learn Alice's `password`

### Authentication Protocol ap3.1

> next idea to fixing ap3.0 is to `encrypt the password`
- by encrypt the password, we can prevent Trudy from learning Alice's password.
- if we assume that Alice and Bob share a `symmetric secret key`
- then Alice can encrypt the password

> `however, the use of cryptography here does not solve the authentication problem`

> Bob is subject to a `playback attack`
> Trudy need only eavesdrop on Alice's communication, `record the encrypted version of the password`

### Authentication Protocol ap4.0

> ap3.0 and ap3.1 results from the fact that
> Bob could not distinguish between the `original authentication` of Alice and the later `playback of Alice's original authentication`
> that is Bob coule not `tell if Alice was live`

- The very (very) observant reader will recall that the `three-way TCP handshake` protocol needed to address the same problem
- the server side of a TCP connection did not want to accept a connection 
- if the `received SYN segment was an old copy (retransmission)` of a SYN segment from an earlier connection.
- How did the TCP server side solve the problem of determining `whether the client was really live`?
- It chose an `initial sequence number` that had not been used in a very long time, 
- sent that number to the client, and then waited for the client to `respond with an ACK segment containing that number`. 
- we can adopt the same idea here for authentication purpose.

- a `nonce` is a number that a protocol will use `only once` in a lifetime.
- that is, `once a protocol uses a nonce, it will never use that number again.`
- our ap4.0 protocol uses a `nonce` as follows:

1. Alice sends the message "I am Alice" to Bob
2. Bob chooses a `nonce, R`, and sends it to Alice.
3. Alice encrypts the `nonce` using Alice and Bob's symmetric secret key
   and sends the `encrypted nonce`.
   the `nonce` is used to ensure that Alice is alive
4. Bob decrypts the received message, if the `decrypted nonce` equals the nonce he sent Alice, then Alice is authenticated
