# Week 7 Submissions Guide — Cloud Heights: The Guard Post

Week 7 is a Deliverable 2 week. The evidence standard is paired: prove what should be allowed and what should be denied, and show the rule that caused those results.

## Labs at a Glance

| Lab | Focus | Required evidence |
|---|---|---|
| 01 — Meet the Guard | protected baseline + editable range | `week07-lab01-security-rules-baseline.png` |
| 02 — Read the Door Ledger | evaluation order + first match | `week07-lab02-evaluation-order.png` |
| 03 — Build the Narrowest Door | Grid Beacon-only TCP 8080 Allow | rule + beacon ALLOWED screenshots |
| 04 — Prove the Guard Works ★ | Deliverable 2 paired proof | final rule + ALLOWED + DENIED screenshots |
| 05 — Break, Explain, Fix | controlled priority fault + remediation | broken, denied, fixed, retest evidence |
| 06 — Logbook / Night Watch | optional evidence-chain analysis | `week07-lab06-evidence-set.png` or reused exact Labs 03–05 files; optional, no penalty if skipped |

## Where Everything Goes

```text
week-07/labs/lab-01-meet-the-guard.md
week-07/labs/lab-02-read-the-door-ledger.md
week-07/labs/lab-03-build-the-narrowest-door.md
week-07/labs/lab-04-prove-the-guard-works.md
week-07/labs/lab-05-break-explain-fix.md
week-07/labs/lab-06-stretch-night-watch.md
assets/screenshots/week-07/
```

## Non-Negotiable Safety

- Never modify any actual protected rule: legacy 100/110/120/1000 or newer 100/110/4096. Both are compatible with the same TCP 8080 exercises.
- Create/edit student rules only in priorities 200–999.
- Never publish a password or Bastion shareable URL.
- Crop browser address bars and login details.
- Use the Lab Portal and your assigned VM, not the Azure Portal.

## Test My Rule Facts

The Portal always tests TCP 8080 to your own VM. Available sources are Grid Beacon `10.60.6.4` and Other Test Source `10.60.6.10`. Start `python3 -m http.server 8080` first. Verdicts are `ALLOWED`, `DENIED`, `SERVICE_NOT_LISTENING`, and `TEST_ERROR`. Wait at least 10 seconds between tests.

## Your Baseline: Legacy or Newer

Your VM has either the legacy four-rule baseline (fallback Deny at priority 1000 for TCP 8080 from the student subnet) or the newer three-rule baseline (explicit `deny-other-inbound` at priority 4096). Both give the same expected results: Grid Beacon `ALLOWED` and Other Test Source `DENIED` once your narrow Allow is in place. Record the rule set your own Portal shows. In Lab 05, choose an unused fault priority lower than your Lab 03 Allow (for example Allow 300 → Deny 250); if your Allow is at 200 or no lower slot is free, ask your instructor first.

## Submitting Your Work

1. Complete each lab worksheet in the Lab Portal and choose **Save Progress**.
2. Upload screenshots to `assets/screenshots/week-07/` in your portfolio repository, using the exact filenames listed in each lab.
3. Choose **Submit to GitHub** for each lab. Submitting one lab does not submit another.
4. **Verify your screenshots:** open the committed worksheet on GitHub and click each image. It should load at full size and be legible, with no password, Bastion shareable URL, browser address bar or login details visible.

### Image links

When a worksheet asks for an image link, paste a **direct image link** — one that opens only the picture, such as a `https://raw.githubusercontent.com/<you>/<repo>/main/assets/screenshots/week-07/<file>.png` link (on GitHub, open the image and use **Raw** or right-click → *Copy image address*). A GitHub file page link containing `/blob/` opens a web page, not the image, so it will not display in your worksheet.

### Lab Submission Tracker

This guide does not add any Lab Submission Tracker steps for Week 7. Your instructor will confirm whether Week 7 needs to be recorded in the Tracker and how; do not create duplicate submissions on your own.

## Notes and Reflection

```text
week-07/notes.md
week-07/reflection.md
```

**Interpreting results:** A TCP connection success proves reachability at that moment, not which rule matched. A timeout marked DENIED means traffic appears blocked; it is not a flow-log verdict and can also reflect a routing or host-firewall problem. SERVICE_NOT_LISTENING means an immediate refusal; check the listener before altering rules. TEST_ERROR is not denial evidence. Each test opens a fresh connection; after a rule change, allow Azure to finish, refresh the ledger and wait at least 10 seconds before retesting. Never invent a successful or denied result.
