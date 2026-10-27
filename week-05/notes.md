# Week 5 Notes — The Grid: Addresses, Names, Ports, and Diagnostics

**Student Name:** Joya Jones

**Date Completed:** 10/27/2026

Summarize this week's key concepts in your own words — not copy-pasted definitions.

## Key Concepts This Week

- IP addresses — the dotted-quad number every device on a network needs (`10.20.5.42` on The Grid)
- The subnet mask — the answer to "which addresses are my neighbours?" (`/24` = `255.255.255.0`)
- The default gateway — the door out of your neighbourhood (`10.20.5.1` on The Grid)
- Private vs public addresses — `10.x`, `172.16–31.x`, and `192.168.x` are *inside* addresses
- DNS — the Grid's Directory Board: a name goes in, an IP address comes out
- NXDOMAIN vs a host that resolves but doesn't answer — two different failures with two different causes
- DHCP — the Address Office: leases, why addresses change, why a laptop "just works" on a new network
- Ports — the numbered doors on a building: 22 SSH, 53 DNS, 80 HTTP, 443 HTTPS, 3389 RDP, 25 SMTP
- TCP vs UDP — a confirmed conversation vs a shout across the room
- The TCP handshake — SYN → SYN-ACK → ACK (packets 7, 8 and 9 in Lab 03)
- The diagnostic toolkit — `ping` (does it answer this test?), `traceroute` (which hops answer?), `dig` (what number is behind that name?). Evidence limits: no ping reply doesn't prove a host is off, and `* * *` means no reply came back, not proof of the exact fault
- **THE LADDER RULE** — check yourself → check your gateway → check the target by NAME → check the target by IP → trace the path. *Work outward, one rung at a time, and let the evidence pick the culprit.*

## My Command Table

You learned the same five jobs twice this week — once in bash, once in PowerShell. Fill the pairs in from memory if you can, and check them afterwards. Type straight into the box below — one job per line, e.g. `show my address: ip addr | ipconfig`. This table is worth keeping.

The bash command and its PowerShell equivalent for each job — show my own address, show my default gateway, test reachability, trace the path, look up a name:

```
show my address: ip addr | ipconfig
show my default gateway: ip route | ipconfig
test reachability: ping | Test-Connection
trace the path: traceroute | tracert
look up a name: dig | Resolve-DnsName
```

## In My Own Words

Your machine has three numbers: an address, a subnet mask, and a default gateway. Explain what each one is for, the way you'd explain it to someone who has never heard those words.

```
My computer's address, also known as an IP address, identifies it as an individual device on the network. The subnet mask tells my computer what part of that address signifies the neighborhood, or local network, and what part belongs to my device only. When my computer wants to communicate with a device that is outside of the local network, it must pass the information to the default gateway, which is another device responsible for identifying where to forward the message.
```

What does DNS actually do? Include the difference between a name that comes back "Name or service not known" (NXDOMAIN) and a name that resolves perfectly well to a host that never answers.

```
DNS stands for Domain Name System, and it's job is to link names to IP addresses. When you execute a DNS lookup on a hostname, two of the possible responses are NXDOMAIN (indicating the name does not exist in the DNS) and the successful return of an IP address. However, knowing the IP address of a device does not mean it will reply to a communication attempt. 
```

An IP address gets your traffic to the right building. What does a port number add to that, and why would a defender care how many doors are open?

```
An IP address may get your traffic to the right building, but the port number allows you to reach the appropriate door for the intended type of communication. For example, if you would like to request a secure connection to a web page, the request must be sent to port 443, which is the standard port for HTTPS. A request to a DNS server would be sent to port 53. Defenders care about the number of open doors because each door is part of the attack surface that someone could target to try to gain access to a networked device.
```

Write out THE LADDER RULE — all five rungs, in order — and say why running them in that order matters more than running them fast.

```
The Ladder Rule provides a proven, reliable, repeatable method for troubleshooting network connections. 1. Check yourself. 2. Check your gateway. 3. Check the target by name. 4. Check the target by IP address. 5. Trace the path. Taking your time and following the steps in order makes troubleshooting a controlled process of elimination, where each step allows us to rule out possible causes before moving on to the next.
```

What is DHCP, and why does your laptop get an address automatically on a network it has never joined before, while a server like `grid-dns` keeps the same address permanently?

```
DHCP stands for Dynamic Host Configuration Protocol, and it is responsible for automatically assigning addresses to devices on a network. When my laptop connects to a new network, DHCP assigns it an available IP address through a temporary, expiring lease, which allows it to work quickly and reliably on network without having to be configured manually. A server like 'grid-dns' needs to keep a stable, static IP address because other devices need to be able to find and communicate with it on a more permanent basis.
```

---

## Submission Checklist

- [x] I summarized each concept in my own words, not copied definitions

- [x] I completed the bash-to-PowerShell command table

- [x] I answered all five "In My Own Words" prompts

- [x] This file is committed to my portfolio repo at `week-05/notes.md`

---

*CyberVisionaries Institute — Cyber Foundations, Tier I*
