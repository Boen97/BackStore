# Public Key Certification

> an important application of `digital signatures` is `public key certification`
> `that is certifying that a **public key belongs to a specific entity**`

- public key certification is used in many popular secure networking protocols, including IPses and `TLS`

## insight into this problem - pizza prank

- Alice is in the pizza delivery business and accepts orders over the Internet
- Bob, a pizza lover, sends Alice a plaintext message that includes his home address and the type of pizza he wants.
- In this message, Bob also includes a digital signature 
- (that is, a signed hash of the original plaintext message) to prove to Alice that he is the true source of the message.
- To verify the signature, Alice obtains Bob’s public key (perhaps from a public key server or from the e-mail message) and checks the digital signature.
- `Trudy is indulging in a prank.`
- `Trudy` sends a message to `Alice` in which she says she is `Bob`, gives Bob’s home address, and orders a pizza. 
- In this message she also includes her `(Trudy’s) public key`

> `digital signature` just check `message authentication`, not the public key certification

- for `public key certification` to be useful, you need to able to verify
- that you have the actual `public key` of `the entity (person, router, browser, and so on)`

> for example, when Alice wants to communicate with Bob using `public key cryptography`
> she needs to verify that the `public key` that is supposed to be Bob's is indeed Bob's 

## CA (Certification Authority)

> binding a public key to a particular entity is typically done by a `Certification Authority(CA)`
> whose job is to validate identites and issue certificates

### a CA has the following roles

1. a CA verifies that an entity is who it say it is.
- when dealing with a CA, one must trust the CA to have performed a suitably rigorous identity verification.

2. once the CA verifies the identity of the entity, the CA creates a `certificate` that binds the public key of the entity to the identity
- the certificate contains the `public key` and `globally unique identifying information` about the owner of the public key.
- the certificate is `digitallly signed by the CA`

> when Bob places his order he also sends his `CA-signed certificate`
> Alice uses the `CA's public key` to check the validity of Bob's certificate and extract `Bob's public key`
