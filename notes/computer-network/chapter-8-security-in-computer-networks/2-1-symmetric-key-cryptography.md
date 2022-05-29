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
