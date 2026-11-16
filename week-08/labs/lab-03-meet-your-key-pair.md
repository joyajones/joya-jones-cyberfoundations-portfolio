# Week 8 Lab 03 — Meet Your Key Pair

**Student Name:** Joya Jones

**Date Completed:** 11/15/2026

**Module:** 3 — Practical Cryptography  
**Submission Path:** `week-08/labs/lab-03-meet-your-key-pair.md`

> ## STOP — Protect secrets
> Never paste, upload, commit, or screenshot a password, passphrase, or private key. Do not run `cat` on any private-key file. Submit only the worksheet and the named screenshots. Keep all cryptographic files on the VM.

## How to Use This Lab

- **[TERMINAL]** means type or paste the command into the Cloud Heights terminal.
- **[WORKSHEET]** means type your response in this lab worksheet.
- Run commands in the order shown. Do not type the sample output.
- If your result does not match the stated success check, stop at the Troubleshooting box. Do not improvise with `sudo`, package installation, Azure settings, or SSH server configuration.

## Mission

Generate a dedicated Week 8 SSH key pair, identify its two files, and record the public-key fingerprint without exposing the private key.

## What You Already Know

The public and private keys have different jobs. The public key may be shared when appropriate. The private key stays under its owner's control. A key passphrase protects the private-key file; it is not the `analyst` account password.

## Lab Environment / Pre-Lab Check

**[TERMINAL] Run:**

```bash
whoami
cf-week8-check
test ! -e ~/.ssh/week8_analyst_ed25519 &&   test ! -e ~/.ssh/week8_analyst_ed25519.pub &&   echo "READY: Week 8 key path is unused" ||   echo "STOP: Week 8 key already exists"
```

**Continue only if:** `whoami` prints `analyst`, all checks report `PASS`, and the final line begins with `READY`.

If the final line begins with `STOP`, do not overwrite the key. Ask the instructor whether to resume with the existing key or use the approved reset.

### If the VM Stops

Return to **My Lab Environment** in the Lab Portal and start your assigned VM. A stopped or deallocated VM is not deleted; saved disk files remain.

## Predict First

**[WORKSHEET]** Which file can be distributed when appropriate: the public key or private key? Explain.

```text
When appropriate, the public key can be distributed. It can be used to encrypt information or verify digital signatures and does not include information about the secret required to decrypt or sign. It is the private key that must not be distributed, as it is the component of a key pair that must remain protected to prevent unauthorized decryption or signing.
```

## Guided Steps

### Step 1 — Prepare the SSH Directory

**[TERMINAL] Run:**

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

### Step 2 — Generate the Key Pair

**[TERMINAL] Run:**

```bash
ssh-keygen -t ed25519 -a 100   -f ~/.ssh/week8_analyst_ed25519   -C "week8-analyst-key"
```

At `Enter passphrase`, create a memorable Week 8 **key passphrase**. Type it again when asked. Nothing may appear while you type; this is normal. Do not use or enter the `analyst` account password unless it happens to be your deliberately chosen key passphrase.

### Step 3 — List the Two Key Files

**[TERMINAL] Run:**

```bash
ls -l ~/.ssh/week8_analyst_ed25519 ~/.ssh/week8_analyst_ed25519.pub
```

**Expected result:** Two filenames appear. The file ending in `.pub` is public. The file without `.pub` is private.

**Evidence moment:** Capture only this listing as `week08-lab03-key-files-permissions.png`.

### Step 4 — Display the Public-Key Fingerprint

**[TERMINAL] Run:**

```bash
ssh-keygen -lf ~/.ssh/week8_analyst_ed25519.pub
```

**Expected result:** A line containing key size, a `SHA256:` fingerprint, the comment `week8-analyst-key`, and `ED25519`.

**Evidence moment:** Capture the fingerprint as `week08-lab03-public-key-fingerprint.png`.

## Stop & Check

Do not run `cat`, `head`, `tail`, `less`, or `nano` on `~/.ssh/week8_analyst_ed25519`.

### Troubleshooting

- `Saving key ... failed`: confirm you are signed in as `analyst`; do not use `sudo`.
- `No such file` in Step 3 or 4: return to Step 2 and check whether key generation completed.
- Existing-key warning: answer `n` and contact the instructor. Never choose overwrite.

## Explain

**[WORKSHEET]** In 3–4 sentences, explain the handling difference between the two files and the purpose of the key passphrase.

```text
The public and private key files must be handled differently because, though related, they have different jobs in establishing and maintaining security. The public key can be distributed when appropriate because sharing it does not compromise the security of the key pair. However, the private key must remain protected and under the owner's control because it is used to decrypt information or create digital signatures. The key passphrase is an optional, additional layer of protection that encrypts the private key file while it is stored.
```

## Analysis Questions

1. Why can the public key be distributed while the private key must remain protected?

```text
The public key can be distributed because it is designed to be shared, and it does not contain the information needed to decrypt data or create digital signatures. The private key must remain protected because it is used to perform those functions, and allowing unauthorized individuals to access it would defeat the purpose of the key pair.
```

2. How is the key passphrase different from the `analyst` account password?

```text
The key passphrase is used to protect the private key file by encrypting it, while the analyst account password is used to authenticate a user logging into the analyst account. They protect different things, and knowing the account password does not automatically provide access to the encrypted private key.
```

3. Why did you use a unique Week 8 filename?

```text
Using a unique Week 8 filename allows us to distinguish this key pair from other keys that may already exist in the system. It also prevents us from accidentally overwriting an existing key pair.
```

## Required Evidence

- `assets/screenshots/week-08/week08-lab03-key-files-permissions.png`
- `assets/screenshots/week-08/week08-lab03-public-key-fingerprint.png`

## Submission Checklist

- [x] The key pair uses the exact Week 8 filenames.

- [x] The private key was never displayed or submitted.

- [x] The fingerprint includes `SHA256:` and `ED25519`.

- [x] Both screenshots use the exact filenames.

- [x] Every worksheet response is complete.

## GitHub / Lab Portal Submission

1. In the Lab Portal, open the matching Week 8 lab.
2. Complete every **[WORKSHEET]** response.
3. Upload only the required screenshots to `assets/screenshots/week-08/`.
4. Select **Submit to GitHub**.
5. Open the committed worksheet and screenshots on GitHub. Confirm they are readable and contain no secrets.

**Never submit:** `.pem` files, files from `~/.ssh/`, passwords, passphrases, private-key contents, or a Bastion shareable URL.
