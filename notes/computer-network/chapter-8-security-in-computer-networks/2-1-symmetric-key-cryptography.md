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
