# Week 6 Lab 05 — Layer Detective

**Student Name:** Joya Jones

**Date Completed:** 11/5/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-05-layer-detective.md`

---

## Overview

**This is a SHORT lab — 20 to 30 minutes — and it needs no VM.** No Cloud Heights session, no simulator, no screenshot. This is a thinking lab: you take the evidence you have already collected in Weeks 5 and 6 and sort it into layers.

This is an **independent** lab.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | This worksheet only — nothing to start, nothing to connect to |
| Prerequisite | Week 5 labs and Week 6 Labs 01–04 |
| Screenshot | None required |

---

## Part A — The Seven-Row Table

Fill in every row. For the last column, name one **real thing you personally saw** in Weeks 5–6 that belongs at that layer.

| # | Layer name | One-line job | Real thing from Weeks 5–6 |
| --- | --- | --- | --- |
| 7 | Application | Handles application-level communication, such as HTTP requests | The readable HTTP request I examined in the Packet Inspector |
| 6 | Presentation | Formats, encodes, and encrypts information so applications can use it | The TLS Client Hello began the process of establishing encrypted communication |
| 5 | Session | Establishes, maintains, and ends ongoing communication between systems | My remote SSH session through Azure Bastion remained active while I ran multiple commands |
| 4 | Transport | Manages communication between machines and directs it to the correct application using port numbers | The TCP three-way handshake ( SYN > SYN-AC > ACK ) |
| 3 | Network | Uses IP addresses and routing info to determine where data needs to go and how to move it between networks | The 'ip route' output showing my default gateway |
| 2 | Data Link | Handles getting data to the next device across the local connection, using MAC addresses | The MAC address shown under eth0 in my 'ip addr' output |
| 1 | Physical | Transmits raw data as electrical, light, or radio signals across a physical connection | The WiFi radio signals used to connect my laptop to the network |

---

## Part B — Case Files

For each case, name the layer where the problem lives, and name the evidence proving the layers **below** it were already working.

### Case File 1 — The Name That Went Nowhere

A hostname lookup fails, but pinging the machine's IP address directly succeeds.

Layer:

```
Application
```

Evidence that the layers below were working:

```
Pinging the IP address directly and receiving a reply confirms that the machine is reachable and that the network path to it is functioning. Since the hostname lookup fails despite successful communication using the IP address, the problem points to DNS at the Application layer.
```

### Case File 2 — Permission Denied

`ssh` to a host returns `Permission denied` after a password prompt.

Layer:

```
Session
```

Evidence that the layers below were working:

```
The password prompt confirms that communication successfully reached the intended machine and the SSH service on port 22. Since the connection made it to the authentication stage, the problem is not with reaching the machine, but with verifying that the user has permission to access it.
```

### Case File 3 — The Cable Story

A machine reports no link on its interface and has no address at all.

Layer:

```
Physical
```

Evidence and reasoning:

```
The machine reporting no link on its network interface suggests that the problem is at the Physical layer, which could also explain why it has no IP address. I would first check that the Ethernet cable is connected properly at both ends, and then look at possible issues with the cable or network port.
```

### Case File 4 — Ping Works, The Page Does Not

`ping` to a server succeeds, but `curl http://<that server>` returns nothing useful.

Layer:

```
Transport OR Application
```

Evidence that the layers below were working:

```
The successful ping confirms that the server is reachable through the network, which is evidence that the Network and lower layers are working. However, I would need to confirm that a connection was established on the HTTP port 80 before determining whether the problem is the HTTP service itself at the Application layer or with establishing the connection at the Transport layer.
```

### Case File 5 — Wrong Neighbourhood

A machine has an address, but its default route points somewhere that cannot forward its traffic.

Layer:

```
Network
```

Evidence and reasoning:

```
Routing is a responsibility of Layer 3, Network. The device at the default gateway may not be equipped or configured to forward traffic to other networks.
```

---

## Part C — The Silent Gateway Case

In Lab 03 the Azure default gateway did not answer your ping. However, your VM had a valid default route configured, and your local communication with the Grid Beacon — the ping replies, the HTTP banner, and `TRACE ID: CF-NET-0604` — succeeded.

A failed gateway ping is one piece of evidence — not automatically proof of a gateway or network failure. But the evidence you weigh against it has to be the right kind of evidence.

The Grid Beacon at `10.60.6.4` sits on the same local subnet as your VM (`10.60.6.0/26`). Reaching it proves **local-subnet connectivity** — that traffic never crosses the default gateway, so beacon success alone cannot prove the gateway forwarded anything. Your `ip route` output proves a **default route is configured** — your VM knows where it intends to send non-local traffic — but it does not prove the gateway forwarded that traffic. The evidence that demonstrates the **default path is functioning** is successful communication with a destination outside `10.60.6.0/26`, such as the outbound internet access through NAT that you examined in Lab 04.

### Step 1 — Rule on the Case

Is the failed gateway ping enough evidence to declare a network-layer failure? Explain your answer using the other evidence you collected. In your response, distinguish between:

- evidence that proves **local-subnet connectivity**
- evidence that proves a **default route is configured**
- evidence that supports **successful off-subnet connectivity**

```
The failed VM gateway ping is not enough evidence to declare a network-layer failure, since this is expected behavior for an Azure-provided default gateway. A successful ping to our known-good target, the Grid Beacon, confirms local-subnet connectivity. Output from 'ip route' proves that a default route is configured. To confirm that the default route is working, I would need to successfully communicate with a destination outside my local subnet, such as accessing the internet through NAT.
```

### Step 2 — Name the Correct Conclusion

For each of these four results, state what it actually proves: the Grid Beacon at `10.60.6.4` answering, the default route shown by `ip route`, a successful connection to a destination outside your local subnet, and the gateway's failed ping. Then state the rule you would give a junior colleague about the difference between an observation ("the gateway did not answer my ICMP probe") and a diagnosis ("the gateway is broken"):

```
The Grid Beacon responding confirms that communication within the local subnet is working. The `ip route` output confirms that a default route is configured, while a successful connection to a destination outside the subnet would demonstrate that the default path is functioning. The gateway's failed ping only tells us that it did not respond to the ICMP request, not that it is broken. I would remind a junior colleague that an observation is simply what a test tells us, while a diagnosis is a conclusion about what is wrong. We need enough supporting evidence before making that conclusion.
```

---

## Part D — Two Models, One Job

The OSI model has seven layers. The practical TCP/IP model most engineers speak day to day has four or five.

### Step 1 — Map Them

Briefly show how the seven OSI layers collapse into the practical model:

```
OSI Layers 7-5 > TCP/IP Application
OSI Layer 4    > TCP/IP Transport
OSI Layer 3    > TCP/IP Internet
OSI Layers 2-1 > TCP/IP Network Access
```

### Step 2 — When Each Is Useful

Explain when the seven-layer vocabulary helps and when the practical model is the better tool:

```
The seven-layer OSI model provides a more detailed way to identify and describe where problems arise in network communication. The TCP/IP model combines those responsibilities into four broader categories, making it easier for a network professional to organize the troubleshooting process. The OSI model is also useful when communicating technical issues, since its language is commonly used in certifications, interviews, and technical documentation.
```

---

## Analysis Questions

**Analysis Question 1.** Explain the Ladder Rule using layer language. What does "test the near thing first" mean when the rungs are layers? *(Minimum 3 sentences.)*

```
The original Ladder Rule tells us to investigate the closest thing first and work our way out. Applied to layers, we are to start from the bottom and work our way up the stack. Troubleshooting progresses from the more fundamental network functions to higher-layer problems.
```

**Analysis Question 2.** Why is "which layer is this?" a faster question than "what is broken?" when you are under pressure? *(Minimum 3 sentences.)*

```
The information we receive about what happened gives us evidence to determine what type of error may be occurring. OSI layer definitions effectively organize error types because we know what each one is supposed to handle. When you're under pressure, you want to follow proven, precise steps and models created to assist troubleshooting, to avoid confusion and error.
```

**Analysis Question 3.** Pick one case file from Part B and describe the very next command you would run to confirm your ruling, and what result would change your mind. *(Minimum 2 sentences.)*

```
For Case File 1, I would use `dig` to test a different, known-good hostname to see whether the DNS problem is limited to the original hostname or affects other lookups as well. If the second hostname resolves successfully, I would investigate whether there is a problem with the original hostname or its DNS record. If the second lookup also fails, I would investigate whether there is a larger problem with DNS.
```

---

## Submission Checklist

- [x] All seven rows of the OSI table completed with a real Week 5–6 anchor each (Part A)

- [x] All five case files given a layer and supporting evidence (Part B)

- [x] Silent gateway case ruled on correctly (Part C)

- [x] OSI vs. practical TCP/IP model compared (Part D)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] No screenshot required for this lab

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-05-layer-detective.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 05: Layer Detective** in the Lab Portal.
2. Fill in the worksheet fields.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-05-layer-detective.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
