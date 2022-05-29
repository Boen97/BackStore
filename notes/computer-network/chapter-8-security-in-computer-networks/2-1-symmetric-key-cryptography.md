# Symmetric Key Cryptography

- all cryptographic alogorithms involve substituing one thing for another.

## Caesar cipher

- a very old, very simple symmetric key alogorithm
- a `cipher` is a method for encrypting data.

- for english text, the `Caesar cipher` would work by taking each letter in the plaintext
- and substituing the letter that is `k` letters later (allowing wraparound, that is letter z follwed by letter a)
- here the value of `k` serves as the key

### monoalphabetic cipher

- an improvement on the `Caesar cipher`
- which also substitutes one letter with another letter
- however, `any letter` can be substitued for any other letter
- as long as `each letter has a unique substitute letter, and vice versa.`

- plaintext letter:
: abcdefghijklmnopqrstuvwxyz

- ciphertext letter:
: mnbvcxzasdfghjklpoiuytrewq

- The plain text message “bob, i love you. Alice”becomes“nkn, s gktc wky. Mgsbc.” 

- knowing that the letters e and t are the most frequently occurring letters in typical English text
- and knowing that particular two-and three-letter occurrences of letters appear quite often together
- make it relatively easy to break this code

- When considering how easy it might be for Trudy to break Bob and Alice’s encryption scheme
- one can distinguish three different scenarios, depending on what information the intruder has.
1. Ciphertext-only attack.
: the intruder has no certain information about the contents of the plaintext

2. Known-plaintext attack
: an intruder knows some of the (plaintext, ciphertext) pairings

3. Chosen-plaintext attack
: the intruder is able to choose the plaintext message and obtain its corresponding ciphertext form.

### polyalphabetic encryption

- Five hundred years ago, techniques improving on monoalphabetic encryption, known as polyalphabetic encryption, were invented
- the idea behind polyalphabetic encryption is to use `muliple monoalphabetic ciphers`

### Block Ciphers

> how symmetric key encryption is done today.

- `block ciphers`, which are used in many secure Internet protocols, including PGP(for secure email)
- `TLS` (for securing TCP connections) and `IPses` for securing the network-layer transport

- in a block cipher, the message to be encrypted is processed in blocks of `k` bits
- for example, if `k=64`, then the message is broken into 64-bit blocks, and each block is encrypted independently.
- To encode a block, the cipher uses a one-to-one mapping to map the k-bit block of cleartext to a k-bit block of ciphertext.

- This block cipher breaks the message up into 3-bit blocks and encrypts each block according to the above mapping.

- `full-table block` ciphers is difficult to implement
- For k = 64 and for a given mapping, Alice and Bob would need to maintain a table with 2^64 input values
- which is an infeasible task
- Moreover, if Alice and Bob were to change keys, they would have to each regenerate the table

- Instead, block ciphers typically use functions that simulate randomly permuted tables.

- Today there are a number of popular block ciphers, including 
- `DES(standard for data encryption standard)` and `3DES` and `AES` (advanced encryption standard)

### Cipher-Block Chaining
- In computer networking applications, we typically need to encrypt `long messages` or long streams of data.
- if we apply a `block cipher`, two or more of the cleartext blocks can be identical
- For these identical blocks, a block cipher would, of course, produce the same ciphertext

- To address this problem, 
- we can mix some `randomness` into the ciphertext so that identical plaintext blocks produce different ciphertext blocks.
- The sender creates a random k-bit number r(i) for the ith block and calculates c(i)
- a new k-bit random number is chosen for each block. 

- introducing randomness solves one problem but creates another: namely, Alice must transmit `twice` as many bits as before.
- block ciphers typically use a technique called `Cipher Block Chaining (CBC)`.
- the basic idea is to `send only one random value along with the very first message`
- and then have the sender and receiver use the computed coded blocks in place of the subsequent random number
