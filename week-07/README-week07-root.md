# CyberFoundations Week 7 — Cloud Heights: The Guard Post

**Module 2 — Networking & Cloud Foundations**

Week 7 moves from reaching and entering a cloud VM to controlling which network sources may reach a service. Students read NIC-level security rules, create one least-privilege TCP 8080 allow, prove both allowed and denied outcomes, troubleshoot a controlled priority fault, and document the evidence.

## Week 7 Labs

1. **Meet the Guard** — inspect the protected baseline and editable range.
2. **Read the Door Ledger** — translate rule fields and apply first-match-wins.
3. **Build the Narrowest Door** — allow only Grid Beacon `10.60.6.4` to TCP 8080.
4. **Prove the Guard Works ★ Deliverable 2** — prove the intended source is allowed and the unintended source is denied.
5. **Break It, Explain It, Fix It** — diagnose and remediate a safe priority failure.
6. **Night Watch — Optional Stretch** — optional evidence-analysis stretch using only Portal-exposed information.

## Protected-Rules Rule

Your room has one of two protected baselines. **Legacy rooms:** 100 `allow-ssh-from-bastion`, 110 `allow-icmp-intra-vnet`, 120 `deny-ssh-student-subnet`, and 1000 `deny-tcp8080-student-subnet` (Inbound Deny TCP 8080 from `10.60.6.0/26`). **Newer rooms:** the same SSH/ICMP allows at 100/110 plus 4096 `deny-other-inbound` (Inbound Deny Any protocol, any source, any port). Read your actual detailed ledger; do not invent missing rules. **Never modify any protected rule.** Student priorities remain **200–999**, before either fallback. Use only inbound TCP 8080 rules from `10.60.6.4` to your assigned VM in Labs 03–05; never create SSH, ICMP, Any-protocol or outbound rules for these exercises. Bastion SSH and ICMP are matched by earlier protected allows. Honest diagnosis of a student-range mistake is not a grading penalty.

## Portfolio Paths

```text
week-07/labs/
assets/screenshots/week-07/
week-07/notes.md
week-07/reflection.md
```

## Access and Evidence Safety

Do not publish passwords or Bastion shareable URLs. Crop browser address bars and login details from every screenshot. Students use the CyberFoundations Lab Portal and their assigned `cf-student-XX` VM; no Azure Portal steps are required.

## Folder Contents

- `week-07/labs/` — six student-facing labs and the submissions guide.
- Instructor review should use the actual baseline and the expected outcomes in each lab; no separate instructor guide is exposed by this portal.
- `notes.md` and `reflection.md` — root copies of student templates.

*CyberVisionaries Institute · CyberFoundations · Tier I*
