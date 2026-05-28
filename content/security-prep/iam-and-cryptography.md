---
title: "Security+ Series: IAM and Applied Cryptography"
date: 2026-05-28
categories: ["Cybersecurity", "Security+"]
tags: ["IAM", "Cryptography", "MFA"]
draft: false
---

## Identity and Access Management (IAM)

The foundation of access control relies on the AAA framework (often IAAA):
1. **Identification:** Claiming an identity (e.g., entering a username).
2. **Authentication:** Proving that identity (e.g., entering a password).
3. **Authorization:** Granting permissions based on the principle of Least Privilege.
4. **Accounting:** Tracking user actions in logs to ensure Non-repudiation.

### Authentication Factors (MFA)
True Multi-Factor Authentication requires combining at least two *different* categories:
* **Type 1: Something you know** (Password, PIN).
* **Type 2: Something you have** (Smartphone, YubiKey, Smartcard).
* **Type 3: Something you are** (Biometrics: Fingerprint, Retina scan).

## Cryptography Essentials

* **Symmetric Encryption:** Uses the *same key* to encrypt and decrypt. It is extremely fast and ideal for encrypting large amounts of data (e.g., AES). Its main drawback is the secure distribution of the key.
* **Asymmetric Encryption:** Uses a *key pair*. The Public Key is shared openly and used to encrypt data. The Private Key is kept secret and used to decrypt data (e.g., RSA, ECC). It is slow but solves the key distribution problem.
* **Hashing:** A one-way mathematical function (e.g., SHA-256) that generates a fixed-length output (digest). It cannot be reversed. Hashing is used to verify data *Integrity*, proving a file or password has not been altered.