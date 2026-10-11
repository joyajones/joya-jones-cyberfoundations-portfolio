# Week 4 Lab — File Permissions: The Badge Audit (CLI Simulator)

**Student Name:** Joya Jones

**Date Completed:** 10/8/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 4  
**Submission Path:** `week-04/labs/lab-01-file-permissions.md`

---

## Overview

Lesson 1 revealed what Ivy's badge rings mean: every file carries permissions — who may read, write, and execute it — and one wrongly-set ring can be a whole security incident. This lab has you run a small permissions audit of your own in the CLI Simulator: read the rings on a set of seeded files (Part A), fix three problems deliberately with `chmod` (Part B), and read the same story on the Windows side with `Get-Acl` (Part C). One screenshot from this lab becomes part of ★ Deliverable 1.

**Nothing here can break anything real.** The CLI Simulator is a consequence-free practice space — exactly the right place to change permissions for the first time.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) — no install, no VM, no real terminal required |
| Shell | Parts A and B **require bash**. Part C **requires PowerShell** (`Get-Acl`). |
| Paths | Simulated Linux-style paths such as `/home/morgan/badge-office` — this is not your real Windows or Mac computer |
| Prerequisite | Week 4, Lesson 1 completed |

**Before you start**

1. Sign in to the Lab Portal and open **Week 4 → CLI Simulator**.
2. Open **Foundry District Badge Office — Bash** (Parts A and B). You will use **Badge Office — PowerShell** later for Part C.
3. Check the prompt. Every challenge starts in `/home/morgan/badge-office`. Type `pwd` if you are unsure.
4. Know about fresh starts. **Every challenge gives you a brand-new copy of the folder** (the divider says `fresh filesystem for this challenge`). Changes from an earlier challenge will not carry over. That is expected — it is not lost work.
5. Know the two kinds of saving. **Next** in the simulator only moves to the next challenge (your simulator progress is saved automatically). Your typed answers in **this worksheet** are saved only when you click **Save Progress** here in the Lab Portal.

**Which challenge goes with which step**

| Simulator challenge | Worksheet step |
|---|---|
| Badge Office — Bash, challenge 1 | Part A, Steps 1–2 |
| Badge Office — Bash, challenge 2 | Part A, Step 3 |
| Badge Office — Bash, challenge 3 | Part B, Step 1 |
| Badge Office — Bash, challenge 4 | Part B, Step 2 |
| Badge Office — Bash, challenge 5 | Part B, Step 3 **and** the Step 4 screenshot |
| Badge Office — PowerShell, challenge 1 | Part C |

---

## Part A — Read the Rings

### Step 1 — Get the Security Report

*Simulator: Badge Office — Bash, challenge 1.*

1. Run the long listing: `ls -l` (`ls -la` also works).
2. Copy the command and the full listing into the boxes below.

This is Week 3's `ls` with one flag added — and that flag turns it into a per-file security report.

Command you ran:

```
ls -l
```

Output (the full listing):

```
-rw-r--r-- 1 morgan foundry  82 badge-codes.txt
-rw-r--r-- 1 morgan foundry  66 cleanup.sh
-rw-rw-rw- 1 morgan foundry 151 master-inventory.txt
-rw-r--r-- 1 morgan foundry  66 shift-notes.txt
-rw-r--r-- 1 morgan foundry  49 supply-list.txt
```

### Step 2 — Decode One File Completely

*Same listing as Step 1 — no new command needed.*

Pick any one file from your listing and decode its full permission string, audience by audience — owner, group, other — the way Lesson 1 decoded `-rwxr-xr--`. Write it as plain-English sentences ("the owner can…, the group can…, everyone else can…").

The file and its permission string:

```
-rw-rw-rw- 1 morgan foundry 151 master-inventory.txt
```

Your plain-English decode:

```
For the master-inventory.txt file, the owner can read and write, the group can read and write, and everyone else can also read and write.
```

### Step 3 — Find the Problem File

*Simulator: Badge Office — Bash, challenge 2.* Run `ls -l` again in this fresh challenge, then read it.

One file in this folder is dramatically more permissive than it should be — every ring lit for every audience, or close to it. Find it. (Hint: scan the *other* triplet — the last three characters — down the whole listing. Which file gives strangers the most?)

The most permissive file and why you flagged it:

```
This is the file that I chose in the first step: the master inventory. I flagged it because every audience can both read and write to it, which looks like a problem.
```

---

## Part B — Change the Rings

This is your first time changing permissions, so we follow THE GATEKEEPER'S RULE on every single change: **check who can touch it now, change it, then check again.** That means `ls -l` before *and after* every `chmod`. The simulator checks the order: a listing that shows the file **before** your first change, and another listing **after** your last change. A change without both checks will not pass.

### Step 1 — Lock Down the Problem File

*Simulator: Badge Office — Bash, challenge 3.*

1. Run `ls -l` (BEFORE).
2. Revoke write from the group (`g-w`) on the problem file from Part A, Step 3.
3. Revoke read and write from other.
4. Run `ls -l` again (AFTER).

Commands you ran (in order, including both ls -l checks):

```
ls -l master-inventory.txt
chmod g-w master-inventory.txt
ls -l
chmod o-rw master-inventory.txt
ls -l
```

The file's permission string BEFORE and AFTER:

```
BEFORE: -rw-rw-rw-
AFTER:  -rw-r-----
```

### Step 2 — Make a Script Runnable

*Simulator: Badge Office — Bash, challenge 4.*

1. Run `ls -l` (BEFORE).
2. Find the script (its name ends in `.sh`). Grant execute to the owner — and only the owner.
3. Run `ls -l` again (AFTER).

Commands you ran:

```
ls -l
chmod u+x cleanup.sh
ls -l
```

Output (the script's corrected permission string):

```
-rwxr--r-- 1 morgan foundry    66 cleanup.sh
```

### Step 3 — Protect the Secrets File

*Simulator: Badge Office — Bash, challenge 5.*

1. Run `ls -l` (BEFORE).
2. Find the file whose name says it should not be readable by everyone. Revoke other's read.
3. Run `ls -l` again (AFTER).

You will stay in this same challenge for the Step 4 screenshot.

Commands you ran:

```
ls -l
chmod o-r badge-codes.txt
ls -l
```

Output (the corrected permission string):

```
-rw-r----- 1 morgan foundry    82 badge-codes.txt
```

### Step 4 — Capture Your Audit Evidence (REQUIRED screenshot)

**Do this inside Badge Office — Bash, challenge 5** (fresh folder, so all three problems are back). This builds one screen that shows the whole audit.

1. Run `ls -l` first. This is your **BEFORE** listing.
2. Replay all three fixes, one after another:

```bash
chmod g-w master-inventory.txt
chmod o-rw master-inventory.txt
chmod u+x cleanup.sh
chmod o-r badge-codes.txt
```

3. Run `ls -l` again. This is your **AFTER** listing.
4. Check the screen. You should see BOTH listings, and the AFTER listing must show all three targets fixed: `master-inventory.txt`, `cleanup.sh` and `badge-codes.txt`. Scroll so all of it is visible.
5. Take a screenshot and save it on your computer as `cli-permissions-audit.png` (lowercase, hyphens, no spaces).

**This screenshot is REQUIRED — it is part of ★ Deliverable 1.** You will upload it and link it in the GitHub Commit section below.

---

## Part C — The Same Story, Windows Edition

### Step 1 — Read One File's Guest List

*Simulator: Badge Office — PowerShell, challenge 1* (starts in `/home/morgan/badge-office`).

1. Run `Get-Acl shift-notes.txt` (or `Get-Acl -Path shift-notes.txt`). Only this file counts for the challenge.
2. Find the **Owner** line and the **Access** line, and copy them below.

On a real Windows computer, `Get-Acl` lists named accounts and their rights. This simulator keeps it short: one Owner line and one Access line. It runs on the same simulated Linux-style folder, not on your real computer.

Command you ran:

```
Get-Acl shift-notes.txt
```

Output (the Owner line and the Access line):

```
Owner : morgan
Access : -rw-r--r--
```

### Step 2 — Translate One Entry

Take the access entry from your output and translate it into plain English, the same way you decoded the Linux string in Part A.

Your plain-English translation:

```
The owner can read and change the file, and both the group and all others can only read the file.
```

---

## Analysis Questions

**Analysis Question 1.** In Part A you found the problem file by scanning the *other* triplet. Why is the "other" audience usually the most important one to audit first on a shared system? *(Minimum 2 sentences.)*

```
The other audience includes all possible users of a shared system outside of the owner and group, including strangers. It is the most important one to audit first because it represents the greatest exposure to the system, where information can be least controlled.
```

**Analysis Question 2.** THE GATEKEEPER'S RULE requires a check before *and* after every change, even though `chmod` rarely fails. What does the *before* check protect you from, and what does the *after* check protect you from? *(Minimum 2 sentences.)*

```
When preparing to use chmod, the before check protects you from changing the wrong file in a list, or making an unnecessary or unintended change in access rights. The after check protects you from granting or revoking access to the wrong or unintended group, or making a syntax mistake that results in no change.
```

**Analysis Question 3.** Lesson 1 called least privilege "granting what's needed and revoking the rest." Pick one of your three fixes from Part B and explain it in least-privilege terms: what was granted that wasn't needed, and who could have taken advantage? *(Minimum 3 sentences.)*

```
The master inventory file originally granted read and write privileges to all users of the shared system. Only those who are responsible for managing and tracking inventory in the business should have read and write access, and those with no related responsibilities should have zero access. Any system user who had motive for making inventory "disappear" and profiting off of that could have tampered with the file to cover their tracks.
```

**Analysis Question 4.** Windows ACLs can name specific people; Linux permissions use three fixed audiences. Describe one situation where the Windows approach would be genuinely more useful — and one cost of that extra flexibility. *(Minimum 2 sentences.)*

```
Windows' approach of naming specific people would be helpful in identifying patterns of suspicious change activity across multiple files. For example, if the same owner is listed across files that were accessed and changed without leadership authorization, an investigator can quickly and easily approach the individual for further examination. One cost of that extra flexibility is that information is not displayed on one single line, which could mean that reporting takes up more screen space or is more cluttered in cases where knowing the owner is not useful.
```

---

## Submission Checklist

- [x] Full `ls -l` listing recorded (Part A, Step 1)

- [x] One file fully decoded in plain English, all three audiences (Part A, Step 2)

- [x] Problem file identified with evidence from its permission string (Part A, Step 3)

- [x] Problem file locked down with before/after `ls -l` checks recorded (Part B, Step 1)

- [x] Script made owner-executable and verified (Part B, Step 2)

- [x] Secrets file protected from other's read and verified (Part B, Step 3)

- [x] **REQUIRED:** `cli-permissions-audit.png` (BEFORE listing, all fixes, AFTER listing) uploaded to `assets/screenshots/week-04/` and its link pasted in the screenshot box below (Part B, Step 4)

- [x] `Get-Acl shift-notes.txt` output recorded and the entry translated (Part C, PowerShell)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-04/labs/lab-01-file-permissions.md`

---

## GitHub Commit Subsection

This lab's written answers are submitted through the **CyberFoundations Lab Portal**. Do the screenshot steps first, then submit.

**📸 REQUIRED — upload your Deliverable 1 screenshot to GitHub**

1. Go to your own portfolio repository on GitHub.com.
2. Open the folder `assets/screenshots/week-04/`. If it does not exist yet, click **Add file → Create new file**, type `assets/screenshots/week-04/README.md`, add one line of text, and click **Commit changes**.
3. Inside `assets/screenshots/week-04/`, click **Add file → Upload files**.
4. Drag in `cli-permissions-audit.png` and click **Commit changes**.

**🔗 Link the screenshot in the portal**

5. On GitHub, click the uploaded file name, then click **Raw** (or the download icon). The image opens on its own.
6. Copy the address from your browser's address bar. It should start with `https://raw.githubusercontent.com/`.
7. Back in the Lab Portal, paste it into the screenshot box labeled **Permissions audit — final ls -l** (just below). A green "Looks like an image address" message and a preview should appear.
   - Do not paste a `github.com/.../blob/...` page link or a file path from your computer — the box will reject them.
   - If your repository is private, the preview may not load. That is fine; the link still points to your image.

**✅ Submit**

8. Click **Save Progress** to save your answers and the link.
9. Connect GitHub if you haven't already (one-time setup) and select your portfolio repo.
10. Click **Submit to GitHub**. The Portal commits this worksheet to `week-04/labs/lab-01-file-permissions.md`. It commits your answers and the image link — not the image file itself, which is why step 4 matters.
11. Open the committed file on GitHub and check that the screenshot shows. If you change anything later, click **Save Progress** and **Submit to GitHub** again.

![Permissions audit — final ls -l](https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/3be0fa5ce1134b6b9f7589f8ba840216327fa3d1/assets/screenshots/week-04/cli-permissions-audit.png)

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
