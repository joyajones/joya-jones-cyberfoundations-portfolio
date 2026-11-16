# Week 8 Lab 04 — Prove Who Signed It

**Student Name:** Joya Jones

**Date Completed:** 11/15/2026

**Module:** 3 — Practical Cryptography  
**Submission Path:** `week-08/labs/lab-04-prove-who-signed-it.md`

> ## STOP — Protect secrets
> Never paste, upload, commit, or screenshot a password, passphrase, or private key. Do not run `cat` on any private-key file. Submit only the worksheet and the named screenshots. Keep all cryptographic files on the VM.

## How to Use This Lab

- **[TERMINAL]** means type or paste the command into the Cloud Heights terminal.
- **[WORKSHEET]** means type your response in this lab worksheet.
- Run commands in the order shown. Do not type the sample output.
- If your result does not match the stated success check, stop at the Troubleshooting box. Do not improvise with `sudo`, package installation, Azure settings, or SSH server configuration.

## Mission

Create a separate signing key pair, sign the incident report, verify the original, then prove that the same signature fails against a changed copy.

## What You Already Know

A digital signature uses a private key to sign and the matching public key to verify. Verification supports integrity and authenticity claims about the key. It does not encrypt the report or prove which human physically used the private key.

## Lab Environment / Pre-Lab Check

**[TERMINAL] Run:**

```bash
whoami
cf-week8-check
cd ~/cloud-heights/week8-cryptography
test ! -e keys/week8_signing_private.pem &&   test ! -e keys/week8_signing_public.pem &&   echo "READY: signing-key paths are unused" ||   echo "STOP: signing-key file already exists"
```

**Continue only if:** `whoami` prints `analyst`, all checks report `PASS`, and the final line begins with `READY`.

If it begins with `STOP`, do not overwrite or delete anything. Ask the instructor whether to resume or reset.

### If the VM Stops

Return to **My Lab Environment** in the Lab Portal and start your assigned VM. A stopped or deallocated VM is not deleted; saved disk files remain.

## Predict First

**[WORKSHEET]** Should the original signature verify after the report content changes? Explain.

```text
The original digital signature should not verify after the report content changes. During the signing process, the signature is bound to the specific content that is being signed.
```

## Guided Steps

### Step 1 — Generate the Private Signing Key

**[TERMINAL] Run:**

```bash
openssl genpkey   -algorithm RSA   -aes-256-cbc   -pkeyopt rsa_keygen_bits:2048   -out keys/week8_signing_private.pem
```

Create one **signing-key passphrase** when prompted. You will use this same passphrase in Steps 2 and 4. Do not record or screenshot it.

### Step 2 — Derive the Public Key

**[TERMINAL] Run:**

```bash
openssl pkey   -in keys/week8_signing_private.pem   -pubout   -out keys/week8_signing_public.pem
```

Enter the signing-key passphrase from Step 1.

### Step 3 — Confirm Both Files Exist

**[TERMINAL] Run:**

```bash
ls -l keys/week8_signing_private.pem keys/week8_signing_public.pem
```

Do not display the private-key contents.

### Step 4 — Sign the Original Report

**[TERMINAL] Run:**

```bash
openssl dgst -sha256   -sign keys/week8_signing_private.pem   -out signatures/incident-report.sig   evidence/incident-report.txt
```

Enter the signing-key passphrase from Step 1.

### Step 5 — Verify the Original Report

**[TERMINAL] Run:**

```bash
openssl dgst -sha256   -verify keys/week8_signing_public.pem   -signature signatures/incident-report.sig   evidence/incident-report.txt
```

**Required result:** `Verified OK`

**Evidence moment:** Capture this result as `week08-lab04-signature-valid.png`.

### Step 6 — Change a Copy

**[TERMINAL] Run:**

```bash
cp evidence/incident-report.txt signatures/incident-report-modified.txt
echo "Change: post-signature modification." >> signatures/incident-report-modified.txt
```

### Step 7 — Test the Original Signature Against the Changed Copy

**[TERMINAL] Run:**

```bash
openssl dgst -sha256   -verify keys/week8_signing_public.pem   -signature signatures/incident-report.sig   signatures/incident-report-modified.txt
```

**Required result:** `Verification failure`. Additional OpenSSL error lines are normal for this intentional failure.

**Evidence moment:** Capture this result as `week08-lab04-signature-invalid-after-change.png`.

## Stop & Check

Do not create the changed copy until Step 5 returns `Verified OK`.

### Troubleshooting

- Step 2 or 4 cannot read the private key: re-enter the Step 1 signing-key passphrase.
- Step 5 reports failure: confirm you used the original report, public key, and signature paths exactly as shown.
- Step 7 reports `Verified OK`: run `tail -n 2 signatures/incident-report-modified.txt`. If the Change line is missing, repeat Step 6 once and rerun Step 7.

## Explain

**[WORKSHEET]** In 4–5 sentences, explain both verification results and why signing is not encryption.

```text
The original report returned "Verified OK" because the digital signature corresponded to the public key used for verification, and the report had not been changed since it was signed. The changed copy returned "Verification failure" because digital signatures are bound to the specific content that was signed. Modifying that content changes its hash completely and invalidates the original signature. Signing is not equivalent to encryption because it provides evidence of the integrity of a file and the key used to sign it, but does not make the file's contents unreadable.
```

## Analysis Questions

1. What does `Verified OK` establish within this lab?

```text
'Verified OK' within this lab establishes that the report being checked was signed using the private key that corresponds to the public key used for verification, and that it has not been changed since signing.
```

2. Why did the changed copy fail verification?

```text
The changed copy failed verification because digital signatures are bound to the specific content that was signed. Changing that content invalidates the original signature.
```

3. Why is the signed report still readable?

```text
The signed report is still readable because digital signature is not equivalent to file encryption. The signing process uses the private key to create a digital signature, but does not encrypt the report's contents.
```

4. Why does the signature alone not prove which human used the private key?

```text
Any individual who has access to the private key is capable of creating digital signatures tied to that key. In a properly secure system, only authorized individuals should have access to the private key, but the signature alone cannot prove which individual actually used it.
```

## Required Evidence

- `assets/screenshots/week-08/week08-lab04-signature-valid.png`
- `assets/screenshots/week-08/week08-lab04-signature-invalid-after-change.png`

## Submission Checklist

- [x] The original returned `Verified OK`.

- [x] The changed copy returned `Verification failure`.

- [x] The private key and passphrase were never displayed or submitted.

- [x] Both screenshots use the exact filenames.

- [x] Every worksheet response is complete.

## GitHub / Lab Portal Submission

1. In the Lab Portal, open the matching Week 8 lab.
2. Complete every **[WORKSHEET]** response.
3. Upload only the required screenshots to `assets/screenshots/week-08/`.
4. Select **Submit to GitHub**.
5. Open the committed worksheet and screenshots on GitHub. Confirm they are readable and contain no secrets.

**Never submit:** `.pem` files, files from `~/.ssh/`, passwords, passphrases, private-key contents, or a Bastion shareable URL.
