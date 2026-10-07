# Week 4 Submissions Guide

How to complete and submit each piece of Week 4 — including your first flagship deliverable. Every item below is graded.

---

## Labs at a Glance

| Lab | What it covers | Submitted via | Required screenshot |
|---|---|---|---|
| Lab 01 — File Permissions: The Badge Audit | Bash `ls -l` + symbolic `chmod` (Parts A–B); PowerShell `Get-Acl` (Part C, required) | Lab Portal → Submit to GitHub | `cli-permissions-audit.png` |
| Lab 02 — The Archive Investigation | **Bash required:** wildcards, `grep`, find → check → lock down (PowerShell challenges are optional practice) | Lab Portal → Submit to GitHub | `cli-search-investigation.png` |
| Lab 03 — Build Your First Virtual Machine ★ | The VM Builder Simulator: wizard, errors, lifecycle, meter | Lab Portal → Submit to GitHub | `vm-config-summary.png` + `vm-dashboard-running.png` |

Each lab file carries its own Submission Checklist — treat those as the source of truth, and check every box before submitting.

---

## ★ Deliverable 1 — VM Concepts + CLI Screenshots

Your first portfolio flagship. It is complete when **all four screenshots** exist in `assets/screenshots/week-04/` with these exact filenames (lowercase, hyphens, no spaces):

1. `cli-permissions-audit.png` — Lab 01, Badge Office Bash challenge 5: BEFORE `ls -l`, the three fixes, AFTER `ls -l`
2. `cli-search-investigation.png` — Lab 02, Archive Investigation Bash challenge 8: search, BEFORE `ls -l`, `chmod`, AFTER `ls -l`
3. `vm-config-summary.png` — Lab 03's Review screen, before Create
4. `vm-dashboard-running.png` — Lab 03's dashboard: Running, with at least one snapshot visible

…and the two VM screenshots are embedded in your committed Lab 03 file.

**Uploading and linking a screenshot**

1. On GitHub.com, open `assets/screenshots/week-04/` in your own portfolio repo (create it on your first upload).
2. **Add file → Upload files** → drag the image in → **Commit changes**.
3. Click the uploaded file, click **Raw**, and copy the address bar (starts with `https://raw.githubusercontent.com/`).
4. Paste it into the lab's screenshot box in the Lab Portal, click **Save Progress**, then **Submit to GitHub**.

Submit to GitHub commits your worksheet and the image link — not the image file, so step 2 is required. Simulator paths like `/home/morgan/archive` are simulated, not on your computer.

**Commit message:** "Add Deliverable 1: VM lifecycle and CLI evidence" — meaningful and descriptive, per your Professional Growth Check.

---

## Notes and Reflection

Both are filled in through the Lab Portal (Week 4 → Notes / Reflection) and committed to `week-04/notes.md` and `week-04/reflection.md`. Same four reflection prompts as every week — consistency is the point.

---

## Common Issues to Avoid

- **Missing "before" checks.** Lab 01 and Lab 02's permission fixes require `ls -l` before AND after each `chmod` — a fix showing only the final state comes back for revision.
- **A pattern that catches too much.** Lab 02, Part A Step 3 requires your output to show the matched files *and nothing extra* — test with `ls` first.
- **Lab 02 is a bash lab.** Parts A–C must be done in Archive Investigation — Bash. The PowerShell Archive challenges are optional practice and do not replace any step.
- **Fresh folder every challenge.** Each simulator challenge starts over, so do each screenshot's whole sequence inside its final challenge.
- **Empty search ≠ absent word.** If `grep denied` returns nothing, check your case before concluding — the logs speak in CAPS.
- **Screenshot 2 in the wrong state.** `vm-dashboard-running.png` must show status **Running** and a snapshot in the list. Stopped, or no snapshot = recapture (the simulator re-runs in minutes).
- **Filename drift.** `vm_config_summary.png` and `VMdashboard.png` are not the spec. Renaming on GitHub takes one minute — exactness is part of the grade.
- **Passwords in worksheets.** Lab 03 never asks for your simulator password. If you typed one anywhere, edit it out before submitting.
- **Refreshing the VM Builder mid-run.** The simulator resets completely on refresh — capture each screenshot when prompted, not later.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
