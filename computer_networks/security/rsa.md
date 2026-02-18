# RSA Algorithm

## Overview

RSA (Rivest-Shamir-Adleman) is a widely-used asymmetric encryption algorithm. It relies on the mathematical difficulty of factoring large prime numbers.

## Key Concepts

### Prime Factorization Problem
- Easy: Multiply two large primes (e.g., 61 × 53 = 3233)
- Hard: Factor the product (e.g., what primes give 3233?)
- RSA security depends on this asymmetry

### Public vs Private Keys
- **Public key**: (e, n) — shared openly
- **Private key**: (d, n) — kept secret
- Mathematical relationship: encryption with public key can only be decrypted with private key

## RSA Key Generation

### Step 1: Choose Two Large Primes
```
p = 61
q = 53
```
*(In practice: 1024-4096 bit primes)*

### Step 2: Compute n
```
n = p × q
n = 61 × 53 = 3233
```
- `n` is the **modulus** (used in both keys)

### Step 3: Compute φ(n) (Euler's Totient)
```
φ(n) = (p - 1) × (q - 1)
φ(n) = 60 × 52 = 3120
```
- φ(n) counts numbers less than n that are coprime to n

### Step 4: Choose Public Exponent e
Requirements:
- 1 < e < φ(n)
- gcd(e, φ(n)) = 1 (e and φ(n) are coprime)

Common choice:
```
e = 65537 (0x10001)
```
- Small, odd, prime
- Fast encryption

Example with small numbers:
```
e = 17 (coprime with 3120)
```

### Step 5: Compute Private Exponent d
Find d such that:
```
(d × e) mod φ(n) = 1
```

Using Extended Euclidean Algorithm:
```
d × 17 ≡ 1 (mod 3120)
d = 2753
```

Verify:
```
(2753 × 17) mod 3120 = 46801 mod 3120 = 1 ✓
```

### Final Keys
```
Public Key:  (e, n) = (17, 3233)
Private Key: (d, n) = (2753, 3233)
```

## RSA Encryption

### Formula
```
Ciphertext = (Message^e) mod n
C = M^e mod n
```

### Example
Encrypt message M = 123:
```
C = 123^17 mod 3233
C = 855
```

## RSA Decryption

### Formula
```
Message = (Ciphertext^d) mod n
M = C^d mod n
```

### Example
Decrypt ciphertext C = 855:
```
M = 855^2753 mod 3233
M = 123 ✓
```

## Modular Exponentiation

Computing large powers efficiently using **repeated squaring**:

### Example: 123^17 mod 3233

```
17 = 16 + 1 = 2^4 + 2^0

123^1 mod 3233 = 123
123^2 mod 3233 = 15129 mod 3233 = 2382
123^4 mod 3233 = 2382^2 mod 3233 = 2188
123^8 mod 3233 = 2188^2 mod 3233 = 2889
123^16 mod 3233 = 2889^2 mod 3233 = 3194

123^17 = 123^16 × 123^1
       = 3194 × 123 mod 3233
       = 855
```

## Digital Signatures with RSA

### Signing (Private Key)
```
Signature = (Hash(Message)^d) mod n
```

### Verification (Public Key)
```
Recovered Hash = (Signature^e) mod n
Compare with Hash(Message)
```

### Process
1. Hash message (SHA-256, etc.)
2. Encrypt hash with private key → signature
3. Anyone can verify with public key

## RSA Security

### Key Size Recommendations

| Key Size | Security Level | Status |
|----------|----------------|--------|
| 512-bit | ~56-bit | **Broken** (1999) |
| 1024-bit | ~80-bit | **Deprecated** |
| 2048-bit | ~112-bit | **Minimum** (current) |
| 3072-bit | ~128-bit | Recommended |
| 4096-bit | ~140-bit | High security |

### Attacks

1. **Factorization**
   - Factor n → recover p, q → compute d
   - Best known: General Number Field Sieve (GNFS)

2. **Small exponent attack**
   - If e is too small and same message sent to multiple recipients
   - Solution: use padding (OAEP)

3. **Timing attack**
   - Measure decryption time to deduce private key
   - Solution: constant-time implementation

4. **Padding oracle attack**
   - Exploit poor padding implementation
   - Solution: use proper padding (PKCS#1 v2.0 - OAEP)

## Practical RSA: Padding

**Never encrypt raw data with RSA!**

### OAEP (Optimal Asymmetric Encryption Padding)
```
Padded = OAEP(Message, Random)
Ciphertext = RSA(Padded)
```

Benefits:
- Randomness (same message → different ciphertext)
- Prevents mathematical attacks
- All-or-nothing decryption

## RSA Limitations

### 1. Speed
- Much slower than symmetric encryption (AES)
- 1000× slower for encryption
- 10,000× slower for decryption

### 2. Size Limit
- Can only encrypt data smaller than key size
- 2048-bit RSA → ~245 bytes max message

### 3. Solution: Hybrid Encryption
```
1. Generate random AES key
2. Encrypt message with AES (fast)
3. Encrypt AES key with RSA (small data)
4. Send both
```

**Example:** TLS/SSL uses this approach

## RSA in Practice

### TLS/SSL
- Server has RSA key pair
- Client verifies server identity (certificate)
- RSA used for key exchange

### SSH
- User has RSA key pair
- Public key on server (~/.ssh/authorized_keys)
- Private key proves identity

### PGP/GPG
- Email encryption
- Each user has RSA key pair
- Web of trust model

### Code Signing
- Software signed with developer's private key
- OS verifies with public key

## Comparison: RSA vs ECC

| Feature | RSA | ECC |
|---------|-----|-----|
| Key Size (112-bit security) | 2048-bit | 224-bit |
| Speed | Slower | Faster |
| Computation | Modular exponentiation | Point multiplication |
| Adoption | Widespread | Growing |
| Quantum threat | Vulnerable | Vulnerable |

## Python Example

```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP

# Generate keys
key = RSA.generate(2048)
public_key = key.publickey()

# Encrypt
cipher = PKCS1_OAEP.new(public_key)
ciphertext = cipher.encrypt(b"Secret message")

# Decrypt
cipher = PKCS1_OAEP.new(key)
plaintext = cipher.decrypt(ciphertext)
```

## See Also

- [Asymmetric Cryptography](asymmetric-crypto.md)
- [RSA Practice Problems](rsa-problems.md)

## Course Materials

- [network_security.pdf](../network_security.pdf)
