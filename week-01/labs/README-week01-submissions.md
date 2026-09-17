# Week 1 — Student Submission Guide

**CyberFoundations · Tier I · Onboarding**

---

## Overview

There's no lab to submit this week — Week 1 has no lab environment. This `labs/` folder exists for consistency with every other week, but it's empty except for this file.

**What you actually need to do this week** is covered in the [Week 1 overview](../README-week01-root.md): create your GitHub account, create this repo from the template, and make your first commit (a short intro in this repo's main `README.md`).

---

## Commit Instructions

Your first commit this week isn't a lab file — it's an edit to this repo's own `README.md`.

**Commit message format:**
```
Week 1: <brief description>
```

Example:
- `Week 1: Add intro to README`

---

### Option 1 — GitHub Web UI

1. Go to **your own** portfolio repository on GitHub.com and open the **Code** tab.
2. In the main file list, open the root [`README.md`](../../README.md) and click the pencil (edit) icon. Do not edit the Week 1 overview for your introduction.
3. Find **About Me**, directly below the main title and **New here?** sentence. Replace only its bracketed instruction paragraph. If the section is missing from your copy, add `## About Me` there, above **This repository documents**.
4. Write at least three sentences: who you are, why you are learning cybersecurity, and one learning goal. Keep all other README content.
5. Click **Preview** to check your introduction and formatting.
6. Click **Commit changes…**, enter `Week 1: Add intro to README`, and select **Commit directly to the main branch** in your own portfolio if available. Ask your instructor if this option is unavailable.
7. Click **Commit changes** in the dialog to save.
8. Reopen the main `README.md` and confirm your introduction appears under **About Me** and the bracketed instruction is gone.

See [Start Here](../../start%20here/START-HERE.md) for an example introduction and a full walkthrough.

The optional Week 1 Practice Worksheet saves to `week-01/practice-worksheet.md`. It is ungraded, does not count toward Week 1 completion, and does not change your root README.

---

### Option 2 — VS Code

1. Open VS Code and open your portfolio repo folder
2. Edit the root `README.md` under **About Me**, using the same placement and three-sentence requirement above
3. Open the **Source Control** panel (Ctrl+Shift+G / Cmd+Shift+G)
4. Stage the change (click **+** next to **Changes**)
5. Enter your commit message
6. Click **✓ Commit**, then **Sync Changes** to push

---

### Option 3 — Git Commands

```bash
cd your-portfolio-repo
git add README.md
git commit -m "Week 1: Add intro to README"
git push
```

---

## Common Issues

| Issue | Fix |
|---|---|
| I don't see a `week-02` folder yet | It's already in this repo — check the repo root. If it's missing, you likely built your repo manually instead of using **Use this template**; recreate it from the template. |
| My repo shows as a fork instead of "generated from" | You used **Fork** instead of **Use this template**. Delete the fork and use the green **Use this template** button instead. |
| I can't find the pencil/edit icon on README.md | Make sure you're logged into GitHub and viewing your own repo, not the original template repo. |

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
