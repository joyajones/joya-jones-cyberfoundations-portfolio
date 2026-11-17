# Week 8 Notes — Practical Cryptography

**Student Name:** Joya Jones

**Date:** 11/16/2026

## Vocabulary in My Own Words

```text
Plaintext: Information in its original, readable form
Ciphertext: Information that has been converted via encryption and can only be made legible with the use of a decryption key
Encryption: The process of converting information into a secure format that is unintelligible without the correct decryption key
Hash / digest: A mathematically derived, fixed-length code that can be compared with another hash to check the integrity of a file
Public key: A shareable key used to encrypt information or verify digital signatures
Private key: A protected key used to decrypt information or create digital signatures
Digital signature: A way of verifying that a private key was used to sign information and that the contents have not been altered
`authorized_keys`: A list of public keys that are approved to access a user account through SSH
```

## Command-to-Purpose Map

| Command | What it demonstrated |
| --- | --- |
| `openssl enc` | Encryption and decryption of data |
| `sha256sum` | How to calculate a file's SHA-256 hash |
| `ssh-keygen` | Generating public and private SSH key pairs |
| `openssl dgst` | How to create and verify digital signatures |
| `ssh ... -o PasswordAuthentication=no` | Establishing an SSH connection without allowing password-based authentication |

## Safety Rules I Must Remember

```text
Rule 1: Protect sensitive information. - Passwords, passphrases, and private keys should never be included in screenshots, uploaded to GitHub, or shared with others.
Rule 2: Maintain proper key custody. - Public keys can be shared when appropriate, but private keys must remain protected and under the owner's control.
Rule 3: Follow established safety procedures. - If a lab produces an unexpected result, stop and follow troubleshooting instructions without making unauthorized changes to the system.
```

## Question for the Instructor

```text
My question for the instructor: We were given a ton of stacked commands to feed into the terminal in this week's labs. I'm wondering what we should be able to retain from that material, and how we can go about learning it?
```
