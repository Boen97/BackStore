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
