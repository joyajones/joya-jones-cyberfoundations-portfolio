# Week 8 Lab 02 — Detect the Change

**Student Name:** Joya Jones

**Date Completed:** 11/15/2026

**Module:** 3 — Practical Cryptography  
**Submission Path:** `week-08/labs/lab-02-detect-the-change.md`

> ## STOP — Protect secrets
> Never paste, upload, commit, or screenshot a password, passphrase, or private key. Do not run `cat` on any private-key file. Submit only the worksheet and the named screenshots. Keep all cryptographic files on the VM.

## How to Use This Lab

- **[TERMINAL]** means type or paste the command into the Cloud Heights terminal.
- **[WORKSHEET]** means type your response in this lab worksheet.
- Run commands in the order shown. Do not type the sample output.
- If your result does not match the stated success check, stop at the Troubleshooting box. Do not improvise with `sudo`, package installation, Azure settings, or SSH server configuration.

## Mission

Create a SHA-256 fingerprint of the original report, change a copy, and prove that the changed copy has a different fingerprint.

## What You Already Know

A cryptographic hash produces a fixed-length digest. Hashing does not hide content and has no decrypt step. A mismatch proves the two inputs differ; it does not identify who made the change.

## Lab Environment / Pre-Lab Check

**[TERMINAL] Run:**

```bash
whoami
cf-week8-check
cd ~/cloud-heights/week8-cryptography
test -f evidence/incident-report.txt && echo "READY: starting file exists"
```

**Continue only if:** `whoami` prints `analyst`, all checks report `PASS`, and the final line is `READY: starting file exists`.

### If the VM Stops

Return to **My Lab Environment** in the Lab Portal and start your assigned VM. A stopped or deallocated VM is not deleted; saved disk files remain.

## Predict First

**[WORKSHEET]** If one line is added to a file, will its SHA-256 digest remain the same? Explain.

```text
If one line is added to a file, its SHA-256 digest will be altogether different from the hash that was created for the original file. This is because SHA-256 takes all of the contents of a file and performs a mathematical operation on that data to produce the digest. The property by which even a small change results in a completely different hash is known as "the avalanche effect."
```

## Guided Steps

### Step 1 — Hash the Original

**[TERMINAL] Run:**

```bash
sha256sum evidence/incident-report.txt | tee hashes/original.sha256
```

**Expected result:** A 64-character hexadecimal digest followed by the original filename.

### Step 2 — Create and Change a Copy

**[TERMINAL] Run:**

```bash
cp evidence/incident-report.txt hashes/incident-report-modified.txt
echo "Review Note: Integrity validation exercise completed." >> hashes/incident-report-modified.txt
tail -n 3 hashes/incident-report-modified.txt
```

**Expected result:** The added `Review Note` appears in the last three lines. The original file was not changed.

### Step 3 — Hash the Changed Copy

**[TERMINAL] Run:**

```bash
sha256sum hashes/incident-report-modified.txt | tee hashes/modified.sha256
```

### Step 4 — Compare the Digest Values

**[TERMINAL] Run:**

```bash
ORIGINAL_HASH=$(cut -d' ' -f1 hashes/original.sha256)
MODIFIED_HASH=$(cut -d' ' -f1 hashes/modified.sha256)
printf 'ORIGINAL: %s
MODIFIED: %s
' "$ORIGINAL_HASH" "$MODIFIED_HASH"
if [ "$ORIGINAL_HASH" = "$MODIFIED_HASH" ]; then
  echo "UNEXPECTED: hashes match — stop and troubleshoot"
else
  echo "EXPECTED: hashes differ because the file changed"
fi
```

**Required result:** Two different digest values and `EXPECTED: hashes differ because the file changed`.

**Evidence moment:** Capture the terminal now as `week08-lab02-sha256-comparison.png`.

## Stop & Check

If you see `UNEXPECTED`, do not submit.

### Troubleshooting

Run `tail -n 3 hashes/incident-report-modified.txt`. If the Review Note is missing, repeat Step 2 once, then repeat Steps 3–4. Do not edit the original file.

## Explain

**[WORKSHEET]** In 3–4 sentences, state what the mismatch proves and two things it does not prove.

```text
The mismatch of SHA-256 hash values produced by the original file vs the edited file proves definitively that a change has been made. It does not prove the degree to which the file has been altered, as there is no relationship between the similarity of files and the hashes that are produced. The SHA-256 digest will be completely different regardless of whether one character or the entire content of a file was changed. The mismatch in hashes also does not prove how many times a file was altered, or by whom.
```

## Analysis Questions

1. What does the different SHA-256 value prove?

```text
The different SHA-256 value proves that the file in question has been altered since the moment of its original hash creation. It does not prove anything about what inside the file has been changed, or the degree to which the contents are different from the original file.
```

2. Why does the mismatch not identify the person who changed the file?

```text
The hash mismatch does not identify the person who changed the file because hashes are derived mathematically based on the contents of the file and do not encode user information. The SHA-256 tool was designed to protect integrity, answering only the question of "has this file been changed" and nothing about ownership.
```

3. Why does hashing not protect confidentiality?

```text
Hashing is not encryption. It produces a digest of a file without changing the accessibility of that same file's contents. The question of whether or not the contents of a file have been changed is unrelated to who can read either the original or edited version.
```

## Required Evidence

- `assets/screenshots/week-08/week08-lab02-sha256-comparison.png`

## Submission Checklist

- [x] The original and changed copy have different digests.

- [x] The required success message appears.

- [x] The screenshot uses the exact filename.

- [x] The original evidence file was not modified.

- [x] Every worksheet response is complete.

## GitHub / Lab Portal Submission

1. In the Lab Portal, open the matching Week 8 lab.
2. Complete every **[WORKSHEET]** response.
3. Upload only the required screenshots to `assets/screenshots/week-08/`.
4. Select **Submit to GitHub**.
5. Open the committed worksheet and screenshots on GitHub. Confirm they are readable and contain no secrets.

**Never submit:** `.pem` files, files from `~/.ssh/`, passwords, passphrases, private-key contents, or a Bastion shareable URL.
