# Week 9 Submissions Guide - Vault Exchange Digital Trust

Week 9 completes Portfolio Deliverable 3: a collection of your work showing what you learned. Complete the two worksheets, add screenshots, and explain the results in your own words. Some checks should refuse deliberately wrong information. That refusal is useful evidence that the check worked.

A **repository** is your project folder on GitHub. A **commit** is a saved set of changes. **Evidence** means the messages, screenshots, and observations that support your explanation. Use the same save/upload method you practiced in Week 7; ask your instructor to demonstrate it if needed.

For both labs, capture at named steps while the result is visible, save reviewed images on your computer. Keep existing filenames for separate captures; one appropriate existing filename is enough for a grouped image. Upload **and commit** reviewed screenshots to `assets/screenshots/week-09/` in your **own connected GitHub portfolio**, not on the VM. Add direct image addresses and captions in the portal, finish answers, Save Progress, Submit to GitHub, and inspect committed Markdown and images.

In the Lab Portal, **Save Progress** stores portal answers. **Submit to GitHub** commits worksheet Markdown and image references only, **not screenshot image bytes**, to your own portfolio. If answers or links change later, Save Progress and Submit to GitHub again. Notes and Reflection are separate worksheets on the Week 9 page and are saved and submitted the same way.

## Labs at a Glance

| Lab | Focus | Required evidence |
|---|---|---|
| 01 - Investigate a Certificate | Read a real website’s digital badge; check its name, dates, and signing offices | Dated observation, completed field/chain tables, fields and chain screenshots |
| 02 - Build and Test Digital Trust | Make a key and badge application; issue and check a badge; try a protected practice connection; explain problems | CSR/certificate/public-key evidence; offline pass/name fail/CA fail; listener/TLS pass/TLS fail/stopped listener; comparison and explanations |

## Where Everything Goes

| File | Repository destination |
|---|---|
| Lab 01 worksheet | `week-09/labs/lab-01-investigate-a-certificate.md` |
| Lab 02 worksheet | `week-09/labs/lab-02-build-and-test-digital-trust.md` |
| Notes | `week-09/notes.md` |
| Reflection | `week-09/reflection.md` |
| Evidence images | `assets/screenshots/week-09/` in your own GitHub repository, not the VM |

Keep exact filenames. In your own GitHub portfolio open `assets/screenshots/week-09/`. If missing, from the repository root choose **Add file > Create new file** named `assets/screenshots/week-09/README.md`, add a description and **Commit changes**. Within the screenshot folder choose **Add file > Upload files**, select reviewed images from your computer and **Commit changes**. Do not change repository visibility. Open each committed image in **Raw** or image view; right-click it and **Copy image address**. Add the direct `https://` image address and caption in the matching portal **Screenshot Links and Captions** box. A GitHub file-view webpage (`github.com/.../blob/...`), local path or repository-relative path is not accepted. Private images may not preview in the portal: check them in your own repository instead of making it public. In a private repository, a copied Raw address ending in `?token=...` expires; use `https://github.com/YOUR-NAME/YOUR-REPO/raw/main/assets/screenshots/week-09/FILENAME.png` instead (it opens for anyone you have given repository access). For Lab 02, a new Submit to GitHub/resubmit checks that all ten required outcome boxes hold usable addresses, not ten unique images, and lists missing/invalid addresses. One shared image URL is accepted in multiple boxes; Save Progress always works, and optional extra boxes may stay blank. Returning to Lab 02 on the VM? Follow its **Returning to This Lab? Start Here** section and continue in your recorded `practice-*` folder; do not start Step 2 again. Existing valid addresses stay valid. Only if manually editing GitHub Markdown, a relative link from a worksheet in `week-09/labs/` opens a repository image; do **not** paste it into portal boxes:

```markdown
![Certificate fields](../../assets/screenshots/week-09/week09-lab01-certificate-fields.png)
```

Add a caption explaining the evidence. Replace this example with the correct filename for each image.

## Readable Evidence Without Repeated Screenshots

- **Lab 02:** ten required outcomes do not mean ten distinct images. Aim for a CSR overview, certificate overview, fingerprint checkpoint, grouped offline checks, readable listener/TLS checkpoints, and stopped-listener checkpoint. More images are optional if text is large or your screen is small. Do not squeeze every result into one tiny image.
- Upload a shared image once, then paste the same direct image address into each existing box it proves. Use each caption to identify its labelled result and real status. Previously submitted split screenshots remain acceptable; no redo or link replacement.
- For CSR details, a readable overview must show subject/SAN and the signature check/message/status. Public-key algorithm/size and signature algorithm may be copied into **CSR public inspection text**.
- For the issued certificate, the overview shows subject/issuer and SAN. Validity dates, key algorithm/size, signature algorithm, Basic Constraints and Key Usage/EKU may be recorded in **Certificate public inspection text**, alongside the observation table. Use actual output; the extra text boxes are not mandatory when existing images/table already cover these details.
- Fingerprint matching, offline pass/wrong-name/wrong-CA, listener state, TLS pass/wrong-name and connection refusal remain screenshot outcomes with actual messages/statuses. Text does not replace these images.
- **Lab 01:** required public certificate fields may be spread between the observation table and one readable overview. Extra field images are optional. Keep the required chain-view evidence.
- Save Progress stores partial answers, image addresses, captions and public text; upload in GitHub stores image bytes; Submit to GitHub commits worksheet Markdown/references and public text, not image bytes. Optional image slots can stay blank. Nothing rechecks or changes past submitted work.
- Keep repositories private if desired. Give your instructor repository access and verify links there; a private image may not preview in the portal. Never publish keys, whole workspace archives or unreviewed verbose logs.

## Portfolio Deliverable 3 Checklist

- [ ] **Certificate investigation:** public hostname, date/time zone, issuer, SAN, validity, key and signature roles, purpose, and chain map in Lab 01.
- [ ] **OpenSSL walkthrough:** dedicated key, request, issuance, inspection, verification, and local connection explained in Lab 02.
- [ ] **Trust evidence:** passing and deliberately failing results with exact CA file and expected name; causes explained.
- [ ] **Comparison:** public website versus isolated service, including who accepts each issuing office and where each service runs.
- [ ] **Reflection:** what certificates establish, their limits, and one evidence-supported troubleshooting decision.
- [ ] **Professional evidence:** legible artifacts, exact filenames, no private material.

## Non-Negotiable Safety

- Keep Week 6-8 work and SSH configuration intact.
- Do not add the practice issuing offices to your computer or browser’s accepted list. The supplied `-CAfile` command option chooses an office only for that check.
- TLS listener remains `127.0.0.1:8443` and is stopped afterward.
- Never upload `.key.pem`, `.ssh` contents, passwords, or access URLs.
- Upload only the named documents and reviewed screenshots. Never upload the whole practice folder or use `git add .` from it; that could include secret keys.

## Submission Sequence

1. Capture required outcomes at named steps while visible. Use compact EVIDENCE boxes in Lab 02; group only clearly labelled results that fit at normal text size. Keep existing filenames for split images or one matching filename for a shared image. Review legibility/privacy.
2. Upload and commit reviewed screenshots to `assets/screenshots/week-09/` in your own GitHub portfolio with **Add file > Upload files** and **Commit changes**.
3. Open each committed image in Raw/image view; reuse its direct address in every outcome box it proves, with a caption naming that specific result. Add narrowly selected public inspection text in Lab 02 if needed; complete both worksheets, notes and reflection in your own words.
4. Press **Save Progress** to store portal answers, then **Submit to GitHub** for each worksheet. The portal commits Markdown and image references, not image files.
5. Inspect committed Markdown and images in GitHub for formatting and privacy. If anything changes later, Save Progress and Submit to GitHub again. Provide the commit link as directed by your instructor.

A missing command, unwritable folder, or VM connection problem should be reported with the exact error. Do not fabricate a passing result. Lab 01 website certificate values are time-sensitive; record your own observation rather than copying a classmate's screenshot.
