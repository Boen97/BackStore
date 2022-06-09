# RSA

- `RSA` algorithm has become almost synonymous with `public key cryptography`

## how RSA works and why it works

- `RSA` makes extensive use of arthmetic operations using `modulo-n` arthmetic

```
[(a mod n) + (b mod n)] mod n = (a + b) mod n 
[(a mod n) - (b mod n)] mod n = (a - b) mod n 
[(a mod n) * (b mod n)] mod n = (a * b) mod n
(a mod n) ^ d mod n = (a ^ d) mod n
```

### example: Alice wants to send to Bob an RSA-encrypted message

- suppose a message is the bit pattern `1001`
- this message can be represented by the decimal integer `9`. 
- when encrypting a message with RSA, it is equivalent to encrypting the `unique integer number` that represents the message.

#### two components of RSA

1. the choice of the public key and the private key.
2. the encryption and decryption algorithm

#### generate the public and private key

-  `Bob` performs the following steps:

1. Choose two `large prime numbers`, `p` and `q`.
   : The larger the values, the more difficult it is to break RSA
   : but the `longer` it takes to perform the `encoding` and `decoding`
   : RSA Laboratories recommends that the `product of p and q` be on the order of `1,024` bits. 

2. compute `n = pq` and `z = (p -1)(q - 1)`

3. Choose a number, `e`, less than `n`, that has `no common factors` (other than 1) with `z`. 
   : In this case, `e` and `z` are said to be `relatively prime`.
   : The letter `e` is used since this value will be used in encryption.
   
4. Find a number, `d`, such that `ed - 1` is exactly divisible (that is, with `no remainder`) by `z`. 
   : The letter `d` is used because this value will be used in `decryption`. 
   : `ed mod z = 1`

5. the publick key KB+ is the pair of numbers `(n, e)`
   the private key KB- is the pair of numbers `(n, d)`

#### the encryption and decryption

- Suppose Alice wants to send Bob a bit pattern represented by the integer number `m` (with `m < n`).
- `c` is encrypted value
```
c = (m ^ e) mod n
```
- `c` is send to Bob

> decryption
- To decrypt the received ciphertext message, c, Bob computes
```
m = (c ^ d) mod n
```

## Session Keys

- `exponentiation` required by RSA is a rather `time-consuming` process
- as a result, RSA is often used in practice in combination with symmetric key cryptography.
- `RSA-encrypted session key`, just use `RSA` to encrypt the shared symmetric key.

## why does RSA works?

- The security of RSA relies on the fact that there are no known algorithms for quickly factoring a number, 
- in this case the public value n, into the primes p and q
- If one knew p and q, then given the public value e, one could easily compute the secret key, d.
- On the other hand, it is not known whether or not there exist fast algorithms for factoring a number, 
- and in this sense, the security of RSA is not guaranteed.
- With recent advances in quantum computing, and published fast factoring algorithms for quantum computers, 
- there are concerns that RSA may not be secure forever
- Another popular public-key encryption algorithm is the Diffie-Hellman algorithm
- `Diffie-Hellman` is not as versatile as RSA in that it cannot be used to encrypt messages of arbitrary length;
- it can be used, however, to establish a symmetric session key, which is in turn used to encrypt messages.
