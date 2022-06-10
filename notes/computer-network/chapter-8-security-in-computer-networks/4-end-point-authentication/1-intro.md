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
