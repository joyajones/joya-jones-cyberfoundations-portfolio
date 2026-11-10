# Week 7 Lab 05 — Break It, Explain It, Fix It

**Student Name:** Joya Jones

**Date Completed:** 11/9/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-05-break-explain-fix.md`

> ## Cloud Heights Protected-Rules Safety Rule
> Your room uses one of two protected baselines. Check your own **INBOUND — EVALUATION ORDER** list to see which one you have:
>
> | Baseline | Protected rules you will see | Fallback for TCP 8080 |
> |---|---|---|
> | **Legacy (four rules)** | 100 `allow-ssh-from-bastion`, 110 `allow-icmp-intra-vnet`, 120 `deny-ssh-student-subnet`, 1000 `deny-tcp8080-student-subnet` | Priority **1000** denies TCP 8080 from `10.60.6.0/26` |
> | **Newer (three rules)** | 100 `allow-ssh-from-bastion`, 110 `allow-icmp-intra-vnet`, 4096 `deny-other-inbound` | Priority **4096** explicitly denies all other inbound traffic (any protocol, source and port) |
>
> **Protected** rules (priorities 100/110, plus 120 and 1000 in legacy rooms, or 4096 in newer rooms) are course infrastructure: they are locked, and you must never modify them. Azure also has built-in default rules (priorities 65000–65500) that the Portal does not list; do not record them unless your ledger actually shows them. **Your editable range is 200–999.** Every student rule is read before either fallback. Write down the rule set your Portal actually shows; do not copy rules from the other baseline or invent missing ones. Use only inbound TCP 8080 rules from `10.60.6.4` to your assigned VM in Labs 03–05; never create SSH, ICMP, Any-protocol or outbound rules for these exercises. Bastion SSH and ICMP are matched by the earlier protected allows at 100/110 in both baselines. Honest diagnosis of a student-range mistake is not a grading penalty.

> **Evidence safety:** Never include a Cloud Heights password or Bastion shareable URL. Crop browser address bars and login information before committing screenshots.

---

## Mission

Create a controlled priority failure inside your student range, diagnose it from evidence, remove the problem, and retest. The goal is method: UNDERSTAND → PREDICT → CHANGE → TEST → VERIFY, then FORECAST → EXECUTE → VERIFY → REMEDIATE → RETEST.

## What You Already Know

A network security rule is a decision about traffic. Rules are evaluated from the lowest priority number to the highest, and the first matching rule wins. Inbound and outbound traffic use separate ledgers. A configured service, a security rule, a test result, and an evidence screenshot answer different questions.

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Required setup | Lab 03 narrow Allow present; listener running |
| Safe failure | Student-created Deny only; every actual protected baseline rule untouched |
| Temporary rule priority | An unused number lower than your Lab 03 Allow, within 200–999 (example: Allow 300 → Deny 250) |
| Time | 45–55 minutes |

- [x] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.

- [x] The VM shows **Running**.

- [x] I can identify every protected rule in my actual baseline (legacy 100/110/120/1000 or newer 100/110/4096).

- [x] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## UNDERSTAND

Your working Lab 03 Allow is at a priority you chose (often 300). A new matching Deny with a **lower** number is evaluated first and makes the later Allow unreachable for that traffic.

**Choose your fault priority before you change anything.**

1. Look up the priority of your Lab 03 Allow in your ledger.
2. Pick an **unused** number that is lower than that Allow and still at least 200. Example: Allow 300 → Deny 250. Allow 450 → Deny 400.
3. **If your Allow is at 200, or every lower number from 200 up is already used, stop and ask your instructor before making any change.** Do not move, edit or delete your Allow on your own, and never reuse an occupied priority.

In the rest of this lab, *your fault priority* means the number you chose here.

## Predict First — FORECAST

Write your Allow priority and your chosen fault priority, then predict Grid Beacon's verdict after adding an inbound Deny for TCP 8080 from `10.60.6.4` at your fault priority, while leaving the working Allow in place.

```text
My Allow rule has a priority of 300, and I have chosen 250 for the temporary fault priority. I predict that Grid Beacon's traffic will be DENIED because the first matching rule will be the Deny at priority 250. Firewall rules are evaluated from the lowest priority number to the highest, and once a match is found, evaluation stops. As such, the Deny rule will be applied before the Allow rule at priority 300 can be reached.
```

## CHANGE / EXECUTE

### Step 1 — Create the Temporary Fault

Create a student rule named `deny-grid-beacon-8080-test`:

- priority: your chosen fault priority — unused, lower than your Lab 03 Allow, and within 200–999
- Inbound / Deny / TCP
- source `10.60.6.4`; source port Any
- destination your assigned VM name or recorded private IP; destination port `8080`
- description: intentional Week 7 troubleshooting fault

Do not edit or delete the Lab 03 Allow. Do not touch any protected rule — your actual fallback (1000 legacy or 4096 newer) stays unchanged throughout this lab.

### Step 2 — Capture the Broken Ledger

Capture both your temporary Deny (at your fault priority) and the later Allow in the same ordered rule view, so the screenshot shows the Deny listed first.

## TEST / VERIFY

Wait at least 10 seconds, select Grid Beacon, and run **Test My Rule**. Expected verdict: `DENIED`.

```text
DENIED - I got the expected verdict with the following message: "No answer at all from port 8080 before the timeout. Traffic from this source appears to be blocked — a network rule may be denying it, or a higher-priority Deny may be matching first." In this case, we know that the higher-priority Deny is matching before an Allow.
```

### Stop & Check — Diagnose Before Fixing

Confirm these healthy facts before remediation:

- VM is Running.
- Python listener is still active on 8080.
- The original Allow is still present and correctly scoped.
- The temporary Deny has a lower priority number than the Allow, so it is evaluated first.

```text
The VM is running and the Python listener is active on 8080, so I can rule out a stopped VM or inactive service. The original Allow is still present, so there is a matching rule that would allow traffic if it were evaluated first. However, the temporary Deny is evaluated first due to its lower priority number.
```

## REMEDIATE

Delete only the temporary `deny-grid-beacon-8080-test` rule you created. Removing the controlled fault returns the ledger to the known-good least-privilege state. Refresh only rereads rules; there is no portal baseline-reset button. Restarting a VM does not reset its rules. To return to the initial baseline after evidence is complete, remove only your own Week 7 student rules, never infrastructure rules. For this lab's retest, keep the narrow Allow and remove only the temporary Deny.

## RETEST

1. Wait at least 10 seconds and retest Grid Beacon: expected `ALLOWED`.
2. Wait at least 10 seconds and retest Other Test Source: expected `DENIED`.

```text
1. ALLOWED
The connection succeeded and your web server answered (HTTP 200\n\n[stderr]\n"}]}). A rule is allowing TCP 8080 from this source.
Source: Grid Beacon (10.60.6.4) · Port TCP 8080

2. DENIED
No answer at all from port 8080 before the timeout. Traffic from this source appears to be blocked — a network rule may be denying it, or a higher-priority Deny may be matching first.
Source: Grid Beacon (10.60.6.4) · Port TCP 8080
```

## Capture Evidence

Your sequence must show broken rules, observed denial, repaired rules, and final retest results.

![Broken rules — week07-lab05-broken-rules.png](https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/f6452e65373bc49ac2c3a796116d298a95b006cd/assets/screenshots/week-07/week07-lab05-broken-rules.png)

![Observed denial — week07-lab05-observed-denial.png](https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/4cd1446c253bfcd4dbe66e9458d7a45273ec9d13/assets/screenshots/week-07/week07-lab05-observed-denial.png)

![Fixed rules — week07-lab05-fixed-rules.png](https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/27388740ffb576866a3173484dabcf5969d51d02/assets/screenshots/week-07/week07-lab05-fixed-rules.png)

![Retest results — week07-lab05-retest-results.png](https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/3ee9a40a9ef79f6550869f30603cd95459716ff4/assets/screenshots/week-07/week07-lab05-retest-results.png)

## Explain — Incident Note

```text
Problem: Grid Beacon unable to reach Python service on VM TCP port 8080.
Evidence: Grid Beacon received no answer from Port 8080 before timeout, which test result details attributed to denial by network rule or higher-priority DENY matching first.
Healthy conditions ruled out: VM is running, stopped VM ruled out.
Python service is active and listening, inactive service ruled out.
Grid Beacon ALLOW rule present in Inbound ledger, missing rule ruled out.
Root cause: Matching Grid Beacon DENY rule at priority number 250 was evaluated before ALLOW rule at priority 300, preventing Allow from being reached.
Remediation: Delete Grid Beacon DENY rule at priority 250.
Retest: Ran test from Grid Beacon and verified Allow result, Grid Beacon reached Python service on Port 8080.
Prevention: Review existing security rules and evaluation order before adding a new rule, to avoid blocking traffic that should be allowed.
```

## Required Evidence

Save screenshots in `assets/screenshots/week-07/`:

- `week07-lab05-broken-rules.png`
- `week07-lab05-observed-denial.png`
- `week07-lab05-fixed-rules.png`
- `week07-lab05-retest-results.png`

Open each image at full size before submission. Confirm that no password, Bastion shareable URL, browser address bar, or unrelated private information is visible.

## Analysis Questions

**Analysis Question 1.** Why did the correct Allow stop working even though it was never edited? (Minimum 4 sentences.)

```text
The correct Allow stopped working, though never edited, because I created a Deny rule with a lower priority number than the Allow. The firewall reads rules from lowest priority number to highest. Once the traffic matched the Deny, the firewall took that action and stopped. The Allow was never reached.
```

**Analysis Question 2.** Why is diagnosing from evaluation order better than changing rules by trial and error? (Minimum 4 sentences.)

```text
Professional troubleshooting follows logic and process rather than trial and error. We already understand how firewall rules are evaluated and how they determine whether traffic is allowed or denied. Since rules are checked in priority order, we can directly determine from that order why a particular rule matched before another. This gives us a logical basis for diagnosing the problem instead of experimenting with changes without understanding what is happening.
```

**Analysis Question 3.** What made this failure safe and recoverable in the course environment? (Minimum 3 sentences.)

```text
The network connection failure was safe because I only changed rules affecting non-essential traffic. Protected rules I was not allowed to modify preserved access to the VM. The failure was recoverable because I could easily remove the temporary deny rule in Azure to restore Grid Beacon's connection to the Python service.
```

## Submission Checklist

- [x] Forecast written before the change

- [x] Temporary fault used an unused priority lower than my Lab 03 Allow and within 200–999 (or I asked my instructor first)

- [x] Broken ledger and DENIED result captured

- [x] VM, listener, and original Allow checked before remediation

- [x] Only the temporary Deny removed

- [x] Grid Beacon retested `ALLOWED` and Other Test Source retested `DENIED`

- [x] Incident note completed

- [x] All protected rules in my actual baseline were left unchanged.

- [x] Every rule I created or edited used priority 200–999.

- [x] No password, Bastion URL, or browser address bar appears in my files.

- [x] This worksheet is committed to `week-07/labs/lab-05-break-explain-fix.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 05: Break It, Explain It, Fix It** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*

**Interpreting results:** A TCP connection success proves reachability at that moment, not which rule matched. A timeout marked DENIED means traffic appears blocked; it is not a flow-log verdict and can also reflect a routing or host-firewall problem. SERVICE_NOT_LISTENING means an immediate refusal; check the listener before altering rules. TEST_ERROR is not denial evidence. Each test opens a fresh connection; after a rule change, allow Azure to finish, refresh the ledger and wait at least 10 seconds before retesting. Never invent a successful or denied result.
