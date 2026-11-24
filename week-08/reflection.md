# Week 8 Reflection — Practical Cryptography

**Student Name:** Joya Jones

**Date:** 11/23/2026

Answer each question in 3–5 sentences.

1. How are encryption and hashing different?

```text
Encryption preserves confidentiality by converting plaintext into ciphertext and requiring a decryption key in order to make the original information readable again. Hashing helps verify integrity by creating a mathematically derived code that represents the exact content of a document. If any part of the content is changed, the hash will be completely different and thus signal that the document received has been altered from the original.
```

2. How are symmetric and asymmetric cryptography different?

```text
Symmetric cryptography is fast and more efficient for encrypting large amounts of data than asymmetric cryptography. The same secret key is used for encryption and decryption when it comes to symmetric, as opposed to the public-private key pairs used in asymmetric cryptography. Asymmetric cryptography allows the public key to be shared openly while the private key remains protected, eliminating the need to share the same secret key between users. Information protected by symmetric keys can become vulnerable if the shared key is compromised, because only one key is needed to lock and unlock.
```

3. Why does a private key need stronger protection than a public key?

```text
A private key needs stronger protection than a public key because it has the power to create digital signatures and decrypt information. If an unauthorized person were to gain access to someone's private key, they could impersonate that individual as presumed owner and originator of signed documents. They could also decrypt information previously encrypted with the corresponding public key. It is safe to share the public key because it only has the capability to verify digital signatures and encrypt information.
```

4. What changed between Week 6 password-based SSH and Week 8 key-based SSH? What stayed the same?

```text
In Week 6, we used the analyst account password to authenticate ourselves when logging in through SSH. However, in Week 8, we used a public and private key pair to complete the authentication process instead. The key passphrase was used to unlock the private key on our client side (the private key never travels), while the server used the public key stored in 'authorized_keys' to verify that the client possessed the corresponding private key. What stayed the same was the SSH protocol, the analyst account, and the destination at localhost on the same VM. The method of authentication changed, but the connection itself remained the same.
```

5. Which Week 8 task felt most connected to a real cybersecurity job, and why?

```text
In Lab 2, we used SHA-256 hashing to detect changes in a file. This task felt most connected to the cybersecurity job that I am looking into because SOC analysts may use hashing to investigate suspicious file modifications. By comparing the hash digests of an original file and a modified version, we were able to establish that the contents were different. 
```

6. What question do you have about certificates, identity, or trust before Week 9?

```text
How important are digital signatures in everyday cybersecurity operations, and what are the most common cases where analysts would need to verify one? I've learned how to create and verify digital signatures, but I want to understand the scope of their practical application. Given that there may be some question as to whether the signature was created by the actual owner of the private key, I also wonder what methods we can use to be more sure.
```
