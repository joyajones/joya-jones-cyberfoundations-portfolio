# How to Create Your Own Week Folder (Week 3 Onward)

**Applies starting Week 3.** `week-01/` and `week-02/` were already built into your repo when you created it from the template. Starting Week 3, you create each new `week-0X/` folder yourself, matching the same structure. No one hands you a `week-03` template — that's intentional. Matching a naming convention consistently on your own is part of what's being evaluated every week from here on.

This guide is a one-time skill. Read it once, and you'll repeat the same few steps every week for the rest of the course.

---

## The Structure You're Matching

Open your existing `week-02/` folder and look at it side by side with this. Every new week folder follows the same shape:

```
week-0X/
├── README-week0X-root.md
├── notes.md
├── reflection.md
└── labs/
    └── README-week0X-submissions.md
    └── lab-0X-[slug].md        (that week's lab file — named in that week's materials)
```

`X` is the week number, always two digits: `03`, not `3`. `[slug]` is a short, lowercase, hyphenated description of the lab (e.g. `lab-03-file-system-navigation.md`) — each week's lab instructions will tell you the exact filename to use.

**`notes.md` and `reflection.md` are the two exceptions — you don't create these by hand.** The Lab Portal delivers both automatically: open that week's Notes and Reflection worksheets in the Portal, fill them in, and click **Submit to GitHub** the same way you do for a lab. The Portal creates the file at `week-0X/notes.md` / `week-0X/reflection.md` for you the first time you submit. This guide's Part A only covers the two files the Portal does *not* create for you: the root README and the labs submissions guide.

You don't need to guess what goes *inside* the root README or submissions guide either — the actual text for both is available to read and copy from the **Reference** section of that week's page in the Lab Portal. This guide only covers building the empty skeleton correctly; the Portal's Reference section has the words that go in it.

---

## Part A — Create the Folder and Files (GitHub Web UI)

No terminal needed. GitHub lets you create nested folders directly by typing a full path into the filename box.

### Step 1 — Open "Create New File"

Go to your portfolio repository on GitHub.com. Click **Add file → Create new file**.

*Why this matters:* GitHub doesn't have a separate "create folder" button — folders only exist once they contain at least one file. Typing a path with a slash in it is how you create both the folder and the file at once.

### Step 2 — Type the Full Path for Your Root README

In the filename box, type:

```
week-03/README-week03-root.md
```

(Replace `03` with the correct week number.) As soon as you type the `/`, GitHub creates the `week-03/` folder automatically.

*Why this matters:* the folder name has to match exactly — lowercase, hyphen, two-digit week number. `Week-03/`, `week-3/`, and `Week3/` are all treated as different, wrong names.

### Step 3 — Paste in the Real Content, Then Commit

Open the Lab Portal, go to that week's page, and open the **Reference** section — you'll find the root README's actual text there, ready to copy. Paste it in, replacing the placeholder. Scroll down, write a commit message like `Week 3: Create week folder`, and click **Commit new file**.

### Step 4 — Repeat for the Submissions Guide

Using the same **Add file → Create new file** method, create:

```
week-03/labs/README-week03-submissions.md
```

This will land inside the `week-03/` folder you already created in Step 2, and will additionally create the `labs/` subfolder the first time you type it. Its content is also in the Lab Portal's Reference section for that week — copy it the same way you did the root README.

*Note:* the actual lab file (e.g. `week-03/labs/lab-03-[slug].md`) comes from your lab work, not from this guide — it's created for you when you submit that lab through the Lab Portal, the same way `notes.md` and `reflection.md` are (see the callout above). Don't hand-create lab files, notes, or reflection — only the root README and submissions guide need manual creation.

---

## Part B — Self-Check Before You Move On

- [ ] Folder is named `week-0X/` — lowercase, hyphenated, two-digit week number
- [ ] `README-week0X-root.md` exists directly inside `week-0X/` (not inside `labs/`), with the real content pasted in from the Lab Portal's Reference section
- [ ] `labs/` is a subfolder inside `week-0X/`, containing `README-week0X-submissions.md` with its content pasted in the same way
- [ ] `notes.md` and `reflection.md` are NOT created by hand — confirm they show up automatically once you submit those worksheets in the Lab Portal
- [ ] Compare side-by-side with `week-02/` — the shape should be identical except for the week number

---

## Common Mistakes

| Mistake | Why it's wrong | Fix |
|---|---|---|
| Named it `week-3` or `Week3` | Breaks the two-digit, lowercase, hyphenated convention every other week uses | Rename by creating the file again with the correct path — GitHub doesn't let you rename a folder directly, only the files inside it |
| Manually created `notes.md` or `reflection.md` | These two are Portal-delivered now — a hand-created blank version will just sit there unless you also submit through the Portal, and you risk it going out of sync with what you actually submitted | Delete the hand-created file; submit that week's Notes/Reflection worksheet in the Lab Portal instead, which creates the file for you |
| Created `week-03` as a single file instead of a folder | Happens if you type `week-03` with no `/` and no filename after it | Delete that file, then recreate using a full path like `week-03/README-week03-root.md` |
| Skipped straight to the lab file without the root README/submissions guide | Every week folder needs both reference files, not just the lab | Go back and create the missing files, pasting content from the Lab Portal's Reference section |

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
