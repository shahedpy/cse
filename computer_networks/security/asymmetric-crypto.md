# Asymmetric Key Cryptography

## Overview

Asymmetric cryptography (also called public-key cryptography) uses a pair of mathematically related keys:
- **Public key** — can be shared openly
- **Private key** — kept secret by the owner

A message encrypted with one key can only be decrypted with the other key.

## How It Works

### Encryption for Confidentiality

```
Alice wants to send secret message to Bob:
1. Alice obtains Bob's public key
2. Alice encrypts message with Bob's public key
3. Only Bob's private key can decrypt the message
4. Bob decrypts with his private key
```

### Digital Signatures for Authentication

```
Alice wants to prove she sent a message:
1. Alice creates hash of message
2. Alice encrypts hash with her private key (creates signature)
3. Bob decrypts signature with Alice's public key
4. Bob compares decrypted hash with hash of received message
5. If they match, message is authentic and from Alice
```

## Key Properties

1. **Computationally infeasible** to derive private key from public key
2. **One-way function** — easy to compute in one direction, hard to reverse
3. **Trapdoor function** — private key is the "trapdoor" that makes reversal easy

## Comparison: Symmetric vs Asymmetric

| Feature | Symmetric | Asymmetric |
|---------|-----------|------------|
| Keys | One shared key | Public/private key pair |
| Speed | Fast | Slower (10-1000x) |
| Key Distribution | Difficult | Easy (public key can be shared) |
| Use Case | Bulk data encryption | Key exchange, signatures |
| Examples | AES, DES | RSA, ECC, DSA |

## Common Asymmetric Algorithms

### RSA (Rivest-Shamir-Adleman)
- Most widely used
- Based on difficulty of factoring large numbers
- Used for encryption and digital signatures

### ECC (Elliptic Curve Cryptography)
- More efficient than RSA
- Smaller keys for equivalent security
- Popular in mobile and IoT

### Diffie-Hellman
- Key exchange protocol
- Allows two parties to establish shared secret over insecure channel
- Does not provide encryption directly

### DSA (Digital Signature Algorithm)
- Signature generation and verification
- Used in SSL/TLS, SSH, PGP

## Applications

1. **Secure communication** (HTTPS/TLS)
2. **Digital signatures** (document signing, code signing)
3. **Key exchange** (establish shared secret for symmetric encryption)
4. **Authentication** (SSH, VPN)
5. **Email security** (PGP, S/MIME)
6. **Blockchain & cryptocurrency** (Bitcoin uses ECDSA)

## Advantages

- **No shared secret** — solves key distribution problem
- **Digital signatures** — authentication and non-repudiation
- **Scalability** — n users need n key pairs (not n² shared keys)

## Disadvantages

- **Slower** than symmetric encryption
- **Key size** — requires larger keys for equivalent security
- **Computational overhead** — not suitable for bulk data encryption

## Hybrid Approach (Best Practice)

Most secure systems use both:
1. **Asymmetric** — exchange symmetric key securely
2. **Symmetric** — encrypt actual data with fast symmetric algorithm

**Example:** TLS/SSL uses RSA or ECDH for key exchange, then AES for data encryption.

## Mathematical Foundation

Asymmetric algorithms rely on mathematical problems that are:
- **Easy in one direction** (encryption)
- **Hard to reverse** without special information (private key)

### Common Hard Problems

1. **Integer Factorization** (RSA)
   - Easy to multiply primes: 53 × 97 = 5141
   - Hard to factor: 5141 = ? × ?

2. **Discrete Logarithm** (Diffie-Hellman, DSA, ElGamal)
   - Easy: 3^x mod p
   - Hard: given y, find x where 3^x ≡ y (mod p)

3. **Elliptic Curve** (ECC)
   - Point multiplication is easy
   - Discrete log on elliptic curve is hard

## See Also

- [RSA (Rivest-Shamir-Adleman)](rsa.md)
- [RSA Practice Problems](rsa-problems.md)

## Course Materials

- [network_security.pdf](../network_security.pdf)
