# Week 4 Lab — The Archive Investigation (CLI Simulator)

**Student Name:** Joya Jones

**Date Completed:** 10/11/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 4  
**Submission Path:** `week-04/labs/lab-02-wildcards-and-searching.md`

---

## Overview

Lesson 2 gave you the Archive's two tools: patterns that match many filenames at once, and the magnet — `grep` — that searches *inside* files. This lab hands you an Archive of your own and a request slip with three jobs on it: match a set of files with patterns (Part A), hunt down a suspicious log entry with grep (Part B), and run the full find → check → lock down audit that combines this week's two lessons into one workflow (Part C). This lab is more independent than Lab 01 — the steps tell you *what* to accomplish, and the *how* is mostly on you. One screenshot from this lab becomes part of ★ Deliverable 1.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) |
| Shell | **Bash is REQUIRED** for Parts A, B and C (Archive Investigation — Bash, challenges 1–8). The four Archive Investigation — PowerShell challenges are **optional extra practice** — they do not replace any bash step, and there is no PowerShell permission-change step. |
| Paths | Simulated Linux-style paths such as `/home/morgan/archive` — this is not your real Windows or Mac computer |
| Prerequisite | Week 4, Lessons 1 and 2 completed; Lab 01 recommended first |

**Before you start**

1. Sign in to the Lab Portal and open **Week 4 → CLI Simulator**.
2. Open **Foundry District Archive Investigation — Bash**.
3. Check the prompt. Every challenge starts in `/home/morgan/archive`, a folder of **11 files** — invoices, logs and notes. Type `pwd` if you are unsure.
4. Know about fresh starts. **Every challenge gives you a brand-new copy of the Archive.** Folders you made or permissions you changed in an earlier challenge will not carry over. That is expected.
5. Know the two kinds of saving. **Next** in the simulator only moves to the next challenge (simulator progress saves automatically). Your typed answers in **this worksheet** are saved only when you click **Save Progress** here in the Lab Portal.

**Which challenge goes with which step**

| Simulator challenge (Bash) | Worksheet step |
|---|---|
| 1 — Survey | Part A, Step 1 |
| 2 — Every invoice | Part A, Step 2 |
| 3 — March invoices only | Part A, Step 3 |
| 4 — Wildcard copy + list | Part A, Step 4 |
| 5 — Search one log | Part B, Steps 1–2 |
| 6 — Search every log | Part B, Step 3 |
| 7 — Find the badge-code file | Part C, Step 1 |
| 8 — Search again, check, change, check | Part C, Steps 2–4 (and the screenshot) |

---

## Part A — Work the Request Slip

### Step 1 — Survey the Archive

*Simulator: challenge 1.* Before filtering anything, run a plain listing of the Archive folder (`ls`). You don't need to record every filename — just note roughly how many files there are and what naming families you can see (invoices, logs, notes…).

What you observed (rough count + the naming families you spotted):

```
About 11 files are listed. Types of files include access logs, invoices, meeting notes, and supply lists.
```

### Step 2 — Match One Family With a Pattern

*Simulator: challenge 2.* The slip's first request: **every invoice file.** Write a pattern that matches all of them and *only* them, and test it with `ls` — remember the habit: pattern first, look at what it catches, then act.

Command you ran (your ls + pattern):

```
ls inv-*.txt
```

Output (the matched files):

```
inv-april.txt
inv-february.txt
inv-january.txt
inv-march-supplement.txt
inv-march.txt
```

### Step 3 — Get Precise

*Simulator: challenge 3.* The slip gets pickier: **only the March invoices**. Refine your pattern so it catches exactly those — no other months and no non-invoice files — you may need a second `*`, a `?`, or a `[ ]` set, depending on how the names are built.

Command you ran:

```
ls inv-march*.txt
```

Output (the matched files — and nothing extra):

```
inv-march-supplement.txt
inv-march.txt
```

### Step 4 — Act on a Pattern

*Simulator: challenge 4* (fresh Archive — make the folder again).

1. Create a folder named `evidence`.
2. Copy **both** March invoices into it with **one** `cp` command that uses your Step 3 pattern. Copy — don't move — so the originals stay put.
3. Confirm with `ls evidence`. You should see exactly the two March invoices.

Commands you ran (mkdir, cp with pattern, confirming ls):

```
ls
mkdir evidence
ls
cp inv-march*.txt evidence
cd evidence
ls
```

---

## Part B — Run the Magnet

### Step 1 — Search One File

*Simulator: challenge 5.* The slip's second request: `door-access.log` records badge events, and somewhere in it are **denied entries**. Search **that one file** with `grep` for the denied entries — and remember the Strict Teacher: the log writes in CAPS, so decide whether you need the case-insensitive flag or the exact capitals. Showing the whole file with `cat` does not count.

Command you ran:

```
grep -i denied door-access.log
```

Output (every matching line):

```
08:12 DENIED badge 2214 east door - retry OK
12:40 DENIED visitor badge front desk
02:47 DENIED badge 4471 storeroom door
```

### Step 2 — Find the Line That Matters

*Same search as Step 1.* Most denied entries are routine — mistyped badges at reasonable hours. One is not. Identify the suspicious line (think: what *time* would worry you?) and record it exactly.

The suspicious line, and why you flagged it:

```
02:47 DENIED badge 4471 storeroom door

Unless we have overnight staff that routinely access the storeroom, the 2AM denied badge is cause for suspicion.
```

### Step 3 — Widen the Sweep

*Simulator: challenge 6.* One log is never the whole story. Re-run your search across **every** `.log` file in one command — a pattern where the filename goes. Note which files your suspicious word appears in.

Command you ran:

```
grep -i denied *.log
```

Which files contained matches:

```
door-access.log:08:12 DENIED badge 2214 east door - retry OK
door-access.log:12:40 DENIED visitor badge front desk
door-access.log:02:47 DENIED badge 4471 storeroom door
west-access.log:13:22 DENIED badge 9911 west door - unknown badge
```

---

## Part C — Find, Check, Lock Down

The slip's last request is the real test: **somewhere in this Archive is a file listing storeroom badge codes.** You don't know its name. You know what's inside it.

### Step 1 — Find It by Its Contents

*Simulator: challenge 7.* Search every `.txt` file for the term `badge-code`, in one command. Record which file comes back.

Command you ran:

```
grep -i 'badge-code' *.txt
```

The file you found:

```
meeting-recap.txt
```

### Step 2 — Check Who Can Touch It

*Simulator: challenge 8* (fresh Archive). Do Steps 2–4 in this order in ONE session so your screenshot tells the whole story:

1. Re-run your Step 1 search across every `.txt` file.
2. Run `ls -l` (BEFORE) and read the found file's rings.

Before you walk away — this is the Week 4 reflex now — read the long listing for that file. Record what you find. Is this file as locked down as its contents deserve?

Command you ran and its output:

```
ls -l meeting-recap.txt

-rw-rw-rw- 1 morgan foundry   129 meeting-recap.txt
```

Your read of the situation:

```
Currently, anyone who is using the shared system can both read and change the file that lists storeroom badge codes. This document should be made private, only accessible by the owner.
```

### Step 3 — Lock It Down

*Still challenge 8.*

3. Change the file's permissions so only its owner can read and write it.
4. Run `ls -l` again (AFTER). The simulator checks this order: search, BEFORE listing, change, AFTER listing.

Commands you ran (including both ls -l checks):

```
ls -l meeting-recap.txt
chmod g-rw meeting-recap.txt
chmod o-rw meeting-recap.txt
ls -l meeting-recap.txt
```

The file's permission string BEFORE and AFTER:

```
BEFORE: -rw-rw-rw-
AFTER:  -rw-------
```

### Step 4 — Capture Your Investigation Evidence (REQUIRED screenshot)

*Still challenge 8.*

1. Scroll so one screen shows the search result, the BEFORE `ls -l`, your `chmod`, and the AFTER `ls -l`.
2. Take a screenshot and save it on your computer as `cli-search-investigation.png` (lowercase, hyphens, no spaces).

**This screenshot is REQUIRED — it is part of ★ Deliverable 1.** You will upload and link it in the GitHub Commit section below.

---

## Analysis Questions

**Analysis Question 1.** In Part A you tested every pattern with `ls` before letting `cp` act on it. Explain what could go wrong if you skipped straight to acting — and why the stakes get higher when the command attached to the pattern is `rm`. *(Minimum 2 sentences.)*

```
Whenever you work in the command line interface, you have to understand that there are no guardrails and no ways to directly "undo" a change that you have made. If you skip straight to acting, there is a greater chance of making a mistake, whether in moving or changing the wrong files, or making another unintended action. It's especially important to check before using the 'rm' command because it serves as the permanent and irreversible deletion.
```

**Analysis Question 2.** Your Part B search returned several routine matches and one suspicious one. In a real security job, why is "reducing six hundred lines to three worth reading" often more valuable than any single answer the search returns? *(Minimum 2 sentences.)*

```
When it comes to investigating a system via the CLI in a real security job, both speed of response and efficiency of commands matter. Especially during a live attack, you want to be able to navigate and detect as quickly as possible, and this includes both using the fewest keystrokes, and getting concise lists of relevant information.
```

**Analysis Question 3.** Part C found a sensitive file by its *contents*, then audited its *permissions*. Explain why neither skill alone would have been enough — what does each half of the workflow catch that the other misses? *(Minimum 3 sentences.)*

```
Knowing exactly what files need to be secured involves two separate skills: 1) identifying sensitive information, and 2) determining who presently has access to those files. The 'grep' search catches the files that may need protecting, given key words that may be present in certain sensitive content, but it cannot give us information about the file's level of exposure. The 'ls -l' command tells us the degree to which files are accessible across users of a system, but it doesn't give an indication of what access is appropriate. Together, the commands show us where to focus attention and action to secure a system.
```

**Analysis Question 4.** The Archive had eleven files; real systems have millions. Which habit from this lab do you think scales up the furthest into professional work, and why? *(Minimum 2 sentences.)*

```
I think the habit of using wildcards scales up the furthest into professional work. I imagine that investigating a system after an incident is like a puzzle, with lots of partial pictures that need to be assembled into a full story. Day to day work may involve fielding requests from system users that only have an "idea" of what they need, or remember parts of relevant information. Wildcards make it possible to search efficiently and successfully with fragments of information. 
```

---

## Submission Checklist

- [x] Archive surveyed and naming families noted (Part A, Step 1)

- [x] Full invoice family matched with a tested pattern (Part A, Step 2)

- [x] Precise single-month pattern built and verified (Part A, Step 3)

- [x] Matches copied to `evidence/` with one pattern-driven `cp` (Part A, Step 4)

- [x] Log searched for denied entries with correct case handling (Part B, Step 1)

- [x] Suspicious line identified with reasoning (Part B, Step 2)

- [x] Multi-file sweep run in one command (Part B, Step 3)

- [x] Hidden file found by contents (Part C, Step 1)

- [x] Its permissions checked and assessed (Part C, Step 2)

- [x] Locked down to owner-only with before/after checks (Part C, Step 3)

- [x] **REQUIRED:** `cli-search-investigation.png` (search, BEFORE, change, AFTER) uploaded to `assets/screenshots/week-04/` and its link pasted in the screenshot box below (Part C, Step 4)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-04/labs/lab-02-wildcards-and-searching.md`

---

## GitHub Commit Subsection

This lab's written answers are submitted through the **CyberFoundations Lab Portal**. Do the screenshot steps first, then submit.

**📸 REQUIRED — upload your Deliverable 1 screenshot to GitHub**

1. Go to your own portfolio repository on GitHub.com and open `assets/screenshots/week-04/` (create it the same way as Lab 01 if it is missing).
2. Click **Add file → Upload files**.
3. Drag in `cli-search-investigation.png` and click **Commit changes**.

**🔗 Link the screenshot in the portal**

4. On GitHub, click the uploaded file name, then click **Raw** (or the download icon). The image opens on its own.
5. Copy the address from your browser's address bar. It should start with `https://raw.githubusercontent.com/`.
6. In the Lab Portal, paste it into the screenshot box labeled **Archive investigation — find, check, lock down** (just below). A green "Looks like an image address" message and a preview should appear.
   - Do not paste a `github.com/.../blob/...` page link or a file path from your computer — the box will reject them.
   - If your repository is private, the preview may not load. That is fine; the link still points to your image.

**✅ Submit**

7. Click **Save Progress** to save your answers and the link.
8. Click **Submit to GitHub**. The Portal commits this worksheet to `week-04/labs/lab-02-wildcards-and-searching.md`. It commits your answers and the image link — not the image file itself.
9. Open the committed file on GitHub and check that the screenshot shows. If you change anything later, click **Save Progress** and **Submit to GitHub** again.

![Archive investigation — find, check, lock down](https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/7a236e7f4da0bbbd3ddb23722e77da9d70f80bad/assets/screenshots/week-04/cli-search-investigation.png)

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
