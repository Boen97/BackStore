# A More Complete Picture

## TLS Handshake

- SSL does not mandate that both to use a specific symmetric key algorithm or a public key algorithm
- instead TLS allows to agress on the `cryptographic algorithms` at the beginning of the TLS session, during the handshake phase

- during the handshake phase, Alice and Bob send `nonces` to each other
- which are used in the creation of the `session keys` (EB, MB, EA, MA)

### The steps of the real TLS handshake

1. the client sends a list of cryptographic algorithms it supports, along with a `client nonce`

2. from the list, the server chooses a `symmetric algorithm`, for example, AES
   and a `public key algorithm (RSA with a specific key length)`
   and a `HMAC algorithm (MD5 or SHA-1)` along with the `HMAC keys`
   it sends back to the client its choices, as well as a `certificate` and a `server nonce`

3. the client `verfies the certificate`, extracts the `sever's public key`
   generates a `Pre-Master Secret(PMS)`, encrypts the PMS with the `server's public key`
   and sends the encrypted PMS to the server.
   
4. using the `same key derivation function` (as specified by the TLS standard)
   the client and server independently compute the `Master Secret (MS)` from the `PMS and nonces`
   the `MS` is then `sliced up` to generate the two encryption and two HMAC keys.

5. the client sends the HMAC of all the handshake messages

6. the server sends the HMAC of all the handshake messages

> the list of algorithms is sent in `cleartext`
> a man-in-the-middle, could `delete the stronger algorithms from the list`
> forcing the client to select a `weak algorithm`

- to prevent such a tampering attack
- the client sends the HMAC of the concatenation of `all the handshake messages` it sent and received.

> why use `nonces` instead of `sequence numbers`

- if someone sniffs all the messages between Alice and Bob
- the `next day`, the guy could send Alice the same sequence of messages on the `previous day`
- if Alice doesn't use `nonce`, she will respond with exactly the same sequence of messages she sent the previous day.

> in summary, in TLS, `nonces` are used to defend against the `connection replay attack`
> and `sequence number` are used to defend against `replaying individual packets during an ongoing session`

## Connection Closure

> using the original `TCP FIN` have `truncation attack` problem
> the guy in the middle could early terminate session

- the solution to this problem is to indicate in the `type field`
- whether the record serves to terminate the TLS session
