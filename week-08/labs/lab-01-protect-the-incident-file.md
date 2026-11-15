# Week 8 Lab 01 — Protect the Incident File

**Student Name:** Joya Jones

**Date Completed:** 11/15/2026

**Module:** 3 — Practical Cryptography  
**Submission Path:** `week-08/labs/lab-01-protect-the-incident-file.md`

> ## STOP — Protect secrets
> Never paste, upload, commit, or screenshot a password, passphrase, or private key. Do not run `cat` on any private-key file. Submit only the worksheet and the named screenshots. Keep all cryptographic files on the VM.

## How to Use This Lab

- **[TERMINAL]** means type or paste the command into the Cloud Heights terminal.
- **[WORKSHEET]** means type your response in this lab worksheet.
- Run commands in the order shown. Do not type the sample output.
- If your result does not match the stated success check, stop at the Troubleshooting box. Do not improvise with `sudo`, package installation, Azure settings, or SSH server configuration.

## Mission

Encrypt a readable incident report, inspect the encrypted file safely, decrypt it, and prove the recovered file is identical to the original.

## What You Already Know

Encryption changes readable **plaintext** into protected **ciphertext**. In this lab, one passphrase protects and recovers the file. Encryption supports confidentiality, but it does not prevent someone from deleting or copying the encrypted file.

## Lab Environment / Pre-Lab Check

| Item | Required value |
|---|---|
| VM | Your assigned `cf-student-XX` VM |
| Linux account | `analyst` |
| Working directory | `~/cloud-heights/week8-cryptography` |
| Starting file | `evidence/incident-report.txt` |
| Estimated time | 25–35 minutes |

**[TERMINAL] Run:**

```bash
whoami
hostname
cf-week8-check
cd ~/cloud-heights/week8-cryptography
pwd
```

**Continue only if:** `whoami` prints `analyst`, the hostname begins with `cf-student-`, every environment check reports `PASS`, and `pwd` ends with `/cloud-heights/week8-cryptography`.

### If the VM Stops

Return to **My Lab Environment** in the Lab Portal and start your assigned VM. A stopped or deallocated VM is not deleted; saved disk files remain.

## Predict First

**[WORKSHEET]** What do you expect to see when encrypted data is inspected as bytes? Why should it not look like the original report?

```text
When encrypted data is inspected as bytes, I expect to see hexadecimal values representing ciphertext instead of the current plaintext report that is now visible. It should not look like the original report because encryption makes the content of any file unintelligible without the decryption key.
```

## Guided Steps

### Step 1 — Confirm the Original Is Readable

**[TERMINAL] Run:**

```bash
cat evidence/incident-report.txt
```

**Expected result:** A readable report beginning with `CLOUD HEIGHTS INCIDENT REPORT`.

### Step 2 — Encrypt the Report

Choose one temporary lab passphrase that you can re-enter during this lab. Do not write it in the worksheet.

**[TERMINAL] Run:**

```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000   -in evidence/incident-report.txt   -out encrypted/incident-report.enc
```

At `enter AES-256-CBC encryption password:`, type the passphrase. Nothing may appear while you type; this is normal. Press Enter, type the same passphrase again, and press Enter.

**Expected result:** The prompt returns without an error message.

### Step 3 — Inspect the Encrypted File

**[TERMINAL] Run:**

```bash
file encrypted/incident-report.enc
xxd -l 64 encrypted/incident-report.enc
```

**Expected result:** `file` identifies data, and `xxd` displays hexadecimal bytes. The readable incident report does not appear.

**Evidence moment:** Capture the terminal now as `week08-lab01-encrypted-inspection.png`.

### Step 4 — Decrypt the File

**[TERMINAL] Run:**

```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000   -in encrypted/incident-report.enc   -out encrypted/incident-report-decrypted.txt
```

Enter the same passphrase from Step 2.

### Step 5 — Prove the Files Match

**[TERMINAL] Run:**

```bash
cmp -s evidence/incident-report.txt encrypted/incident-report-decrypted.txt   && echo "MATCH: decrypted file equals original"   || echo "MISMATCH: stop and troubleshoot"
```

**Required result:** `MATCH: decrypted file equals original`

**Evidence moment:** Capture the terminal now as `week08-lab01-decryption-match.png`.

## Stop & Check

Do not submit unless both required evidence moments succeeded.

### Troubleshooting

- `bad decrypt` or `bad password read`: rerun Step 4 and enter the exact Step 2 passphrase.
- `No such file or directory`: run `cd ~/cloud-heights/week8-cryptography`, then rerun the failed step.
- `MISMATCH`: delete only the decrypted copy with `rm -f encrypted/incident-report-decrypted.txt`, then repeat Steps 4–5.

## Explain

**[WORKSHEET]** In 3–4 sentences, explain how this lab demonstrates confidentiality and why encryption does not prevent deletion.

```text
The Confidentiality principle of the CIA triad asserts that information should only be accessible to authorized individuals. In this lab, we found a file that was legible to anyone who had access to it, and we were able to apply encryption to protect its contents. Only those holding the decryption passphrase moving forward will be able to read the encrypted copy. Encryption does not prevent deletion because that is not what the tool was designed to do; it does not change user access rights, which may in some cases be used to protect against non-administrator file deletion.
```

## Analysis Questions

1. Why can an encrypted file still be copied or deleted?

```text
An encrypted file can still be copied or deleted because the process of encryption only changes the readability of data and does not limit user file access rights. The encryption process was created to preserve the confidentiality of content and does not prevent the file itself from being copied or deleted.
```

2. What job did the passphrase perform?

```text
The passphrase performed the job of enabling decryption, effectively reversing the encryption function and making the data legible again. However, it is important to distinguish the passphrase from the key itself. It provides the secret needed for the system to derive a key in the background, but it is not the key.
```

3. Why does the match test prove correct recovery but not prove who handled the file?

```text
The match test compares the document's decrypted contents to its pre-encrypted form and can tell whether the information changed. This test does not have the capability to check what users have interacted with the file, or what actions those users might have taken.
```

## Required Evidence

Save exactly these files in `assets/screenshots/week-08/`:

- `week08-lab01-encrypted-inspection.png`
- `week08-lab01-decryption-match.png`

## Submission Checklist

- [x] Both required results appeared.

- [x] Both screenshots use the exact filenames above.

- [x] No passphrase or other secret appears.

- [x] Every worksheet response is complete.

- [x] The worksheet is saved at the stated submission path.

## GitHub / Lab Portal Submission

1. In the Lab Portal, open the matching Week 8 lab.
2. Complete every **[WORKSHEET]** response.
3. Upload only the required screenshots to `assets/screenshots/week-08/`.
4. Select **Submit to GitHub**.
5. Open the committed worksheet and screenshots on GitHub. Confirm they are readable and contain no secrets.

**Never submit:** `.pem` files, files from `~/.ssh/`, passwords, passphrases, private-key contents, or a Bastion shareable URL.
