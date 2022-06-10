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
   : once the three-way TCP handshake is finished, Bob sends Alice a hello messge
   : `Alice` responds with her `certificate`, which contains her public key.
   
2. verify that Alice is really Alice
   : the `certificate` has been certified by a `CA`, it is for sure that the public key belongs to `Alice`
   
3. send Alice a `master secret key`, which will be used by both Alice and Bob to generate all the `symmetric keys`
   they need to for the TLS session.
   : Bob generate a `Master Secret(MS)` which will only be used for this TLS session
   : Bob `encrypts` `MS` with `Alice's public key` to create the `(EMS) encrypted master secret`
   : send `EMS` to Alice
   : Alice decrypts the `EMS` with her `private key` to get the `MS`
   : then Botn Bob and Alice know the master secret for this TLS session.

## Key Derivation

- Alice and Bob could use the `shared MS` as the `symmetric session key` for all subsequent `encryption and data integrity checking`
- but it's `more safer` to use different `cryptographic keys`
- and also use `different keys` for `encryption and integrity checking`

- thus, both Alice and Bob use the `MS` to generate `four keys`

1. `Eb` = session encryption key for data send from Bob to Alice.
2. `Mb` = seesion `HMAC key` for data sent from Bob to Alice.
   where `HMAC` is a standard `hashed` message authentication code (`MAC`)
3. `Ea` = session encryption key for data send from Alice to Bob.
4. `Ma` = session `HMAC key` for data sent from Alice to Bob.

- Alice and Bob each generate the four keys from the `MS`
- at the end of the key derivation phase, both Alice and Bob have all the `four keys`
- `two encryption keys` will be used to encrypted data;
- `two HMAC keys` will be used to verify the integrity of the data;

## Data Transfer

- since TCP is a `byte-stream` protocol, a natural approach for TLS to `encrypt application data` `on the fly`
- and then pass the encrypted data on the fly to `TCP`

- but if we encrypt data on the fly, where would we put the `HMAC` for the `integrity check`?
- to address this issue, TLS `breaks` the data stream into `records`, `appends` an `HMAC` to each record for `integrity checking`
- and encrypts the `record + HMAC`

- to create the `HMAC`, Bob inputs the `record data along with the key Mb` info a `hash function`.
- and then use `Eb` to encrypt the `package record + HMAC`
- then send this encrypted package to TCP

- although this approach goes a long way, it still isn't bullet-proof when it comes to providing `data integrity` 
- for the `entire message stream`
- the intruder could `capture two segaments sent by Bob, reverse the order of the segments, adjust the TCP sequence number (which are not encrypted)`
- the solution to this problem, is to use `sequence number`;

- TLS does this as follows:
1. Bob maintains a `sequence number counter`, which begins at zero and is `incremented for each TLS record he sends`
: Bob doesn’t actually include a sequence number in the record itself, 
  but when he `calculates the HMAC`, he `includes the sequence number` in the `HMAC calculation`
: Thus, the `HMAC` is now a `hash of the data` plus the `HMAC key` plus the `current sequence number`
: `Alice tracks Bob’s sequence numbers`, 
: allowing her to verify the data integrity of a record by `including the appropriate sequence number in the HMAC calculation`.
