# 🔐 CryptoLab

> A comprehensive Python cryptography suite covering classical to modern encryption algorithms, built for educational and portfolio purposes. Features a full-screen terminal-themed GUI and an interactive CLI.

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue?logo=python)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Algorithms](https://img.shields.io/badge/Algorithms-17%2B-purple)]()

---

## Quick Start

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Launch the GUI application
python cryptolab_gui.py

# 3. Or launch the interactive CLI
python main.py
```

---

## Algorithm Coverage

| Category | Algorithms |
|---|---|
| **Classical** | Caesar, Hill (2×2 / 3×3), Vigenère, One-Time Pad |
| **Symmetric** | RC4, DES, Triple-DES, AES-128/192/256 (ECB / CBC / CTR / GCM), AES Finalists |
| **Asymmetric** | RSA-2048 (OAEP), Diffie-Hellman (MODP), ElGamal, ECDH (P-256), ECIES |
| **Hashing** | MD5, SHA-1/256/512, SHA-3, HMAC-SHA256, pure-Python SHA-256 |
| **Signatures** | RSA-PSS, PKCS#1 v1.5, ECDSA (P-256), DSA, ElGamal Signatures |
| **Protocols** | Paillier Homomorphic Encryption, TCP/UDP encrypted chat, Homomorphic voting |

### Security Demonstrations (Educational)

| Attack / Weakness | Module |
|---|---|
| Caesar brute-force + frequency analysis | `classical/caesar.py` |
| Vigenère Kasiski + IC cryptanalysis | `classical/vigenere.py` |
| Hill cipher known-plaintext attack | `classical/hill.py` |
| OTP key-reuse → crib-dragging | `classical/otp.py` |
| AES-ECB structure leak (image demo) | `symmetric/aes_cipher.py` |
| AES-CBC 1-bit avalanche propagation | `symmetric/aes_cipher.py` |
| AES-CTR nonce-reuse → C1⊕C2=M1⊕M2 | `symmetric/aes_cipher.py` |
| RSA textbook (no padding) | `asymmetric/rsa_cipher.py` |
| Diffie-Hellman MITM simulation | `asymmetric/diffie_hellman.py` |
| ElGamal malleability: forge E(2M) | `asymmetric/elgamal.py` |

---

## Project Structure

```
CryptoLab/
├── cryptolab_gui.py          # GUI application (primary entry point)
├── main.py                   # Interactive CLI (secondary entry point)
├── requirements.txt          # Python dependencies
├── README.md                 # Project documentation
├── pyrightconfig.json        # VS Code / Pylance static analysis config
│
├── .vscode/
│   └── settings.json         # Extra Python paths for VS Code
│
├── classical/                # Classical cipher implementations
│   ├── caesar.py             # Brute-force + frequency analysis
│   ├── hill.py               # 2×2 / 3×3 matrix cipher + known-plaintext attack
│   ├── otp.py                # One-Time Pad + key-reuse vulnerability + crib-drag
│   └── vigenere.py           # Kasiski + IC cryptanalysis
│
├── symmetric/                # Symmetric block and stream ciphers
│   ├── rc4.py                # RC4 stream cipher (educational, deprecated)
│   ├── des_cipher.py         # DES / Triple-DES
│   ├── aes_cipher.py         # AES-128/192/256 with mode comparisons + attacks
│   └── aes_finalists.py      # Rijndael, Twofish, Serpent, RC6, MARS benchmarks
│
├── asymmetric/               # Public-key cryptography
│   ├── rsa_cipher.py         # RSA-OAEP + hybrid RSA+AES encryption
│   ├── diffie_hellman.py     # DH key exchange + MITM + ECDSA-authenticated DH
│   ├── elgamal.py            # ElGamal probabilistic encryption + malleability
│   ├── ecc.py                # Elliptic-curve: tiny curve demo, ECDH, ECIES
│   └── signature.py          # RSA-PSS, ECDSA (P-256), DSA, ElGamal signatures
│
├── hashing/                  # Hash function implementations
│   ├── sha_hash.py           # MD5 / SHA-* wrappers + avalanche + benchmarks
│   └── sha256_pure.py        # Pure-Python SHA-256 (FIPS 180-4 reference impl.)
│
├── protocols/                # High-level cryptographic protocols
│   ├── homomorphic.py        # Paillier homomorphic encryption (add, scalar mul)
│   └── signature.py          # Full signature suite (RSA-PSS/ECDSA/DSA/EdDSA)
│
└── utils/                    # Shared mathematical primitives
    ├── math_utils.py         # GCD, modular inverse, Euler totient
    ├── primes.py             # Miller-Rabin primality, safe primes, generators
    └── converter.py          # bytes ↔ int ↔ hex ↔ text conversion helpers
```

---

## Dependencies

| Package | Version | Purpose |
|---|---|---|
| `pycryptodome` | ≥ 3.20 | AES, DES, RSA, DSA, ECDSA, SHA-* primitives |
| `sympy` | ≥ 1.12 | Large prime generation and modular arithmetic |
| `numpy` | ≥ 1.24 | Hill cipher matrix operations and image comparison demos |
| `cryptography` | ≥ 41.0 | Supplementary elliptic-curve support (ECDH, EdDSA) |

```bash
pip install -r requirements.txt
```

---

## Usage Examples

### GUI

```bash
python cryptolab_gui.py
# → Opens the full-screen terminal-themed GUI
```

### CLI

```bash
python main.py
# → Interactive numbered menu covering all modules
```

### Programmatic API

```python
# Caesar cipher
from classical.caesar import encrypt_caesar, decrypt_caesar
ct = encrypt_caesar("Hello World", shift=13)

# AES-256-GCM
from symmetric.aes_cipher import encrypt_text, decrypt_text
params = encrypt_text("Top secret", mode="GCM")
plain  = decrypt_text(params)

# RSA-OAEP
from asymmetric.rsa_cipher import generate_keypair, encrypt_oaep, decrypt_oaep
priv, pub = generate_keypair(2048)
ct  = encrypt_oaep(b"Secret message", pub)
msg = decrypt_oaep(ct, priv)

# Paillier homomorphic encryption
from protocols.homomorphic import Paillier
p   = Paillier(bits=512)
ct_a, ct_b = p.encrypt(42), p.encrypt(17)
print(p.decrypt(p.add_ciphertexts(ct_a, ct_b)))  # → 59
```

---

## Academic Context

This project was developed as part of a 3rd-year Cybersecurity curriculum, covering classical and modern cryptographic algorithms with deliberate implementations of known vulnerabilities for educational purposes. Every attack demonstration is clearly labelled and is not intended for use against real systems.

---

## License

MIT — free to use, modify, and distribute with attribution.
