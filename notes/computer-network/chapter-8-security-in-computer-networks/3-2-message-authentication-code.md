# Message Authentication Code.

1. Alice creates message m and calculates the hash H(m) (for example, with SHA-1).
2. Alice then appends H(m) to the message m, creating an extended message
   (m, H(m)), and sends the extended message to Bob.
3. Bob receives an extended message (m, h) and calculates H(m). If H(m) = h,
   Bob concludes that everything is fine.

- This approach is obviously flawed.
- everyone can create a bogus message m' in which he says he is Alice.

- to perform `message integrity`, Alice and Bob will need a `shared secret s`
- this `shared secret`, which is nothing more than a `string of bits`, is called the `authentication key.`

1. Alice create message `m`, concatenates `s` with `m` to create `m + s`
   and calculates the hash `H(m + s)` (for example, with `SHA-1`)
   `H(m + s)` is called the `message authentication code (MAC)`

2. Alice append the `MAC` to the message `m`, creating an extended message `(m, H(m + s))`
   and send the extended message to Bob.

3. Bob receives and extended message `(m, h)` and knowning `s`
   calculates the `MAC H(m + s)` if `H(m + s) = h`, then the message integrity is fine.

> `One nice feature of a MAC is that it does not require an encryption algorithm.`

- in many applications, including the link-state routing algorithm described earlier
- `only concerned with message integrity`, and not concerned with `message confidentiality`

> Using a `MAC`, the entities can authenticate the messages they send to each other 
> without having to `integrate complex encryption algorithms` into the integrity process.

> a number of `different standards for MACs` have been pro- posed over the years. 
- most popular standard today is `HMAC`, which can be used either with `MD5 or SHA-1`
- HMAC actually runs data and the authentication key through the hash function `twice`


## an issue

> `How do we distribute the shared authentication key to the communicating entities?`
- For example, in the link-state routing algorithm, 
- we would somehow need to distribute the secret authentication key to each of the routers in the autonomous system.
- A network administrator could actually accomplish this by physically visiting each of the routers.
- Or, if the network administrator is a lazy guy, and if each router has its own public key
- the network administrator could distribute the authentication key to any one of the routers by 
- encrypting it with the router’s public key and then sending the encrypted key over the network to the router.
