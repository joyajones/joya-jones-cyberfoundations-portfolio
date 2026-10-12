# Week 4 Notes — Permissions, Searching, and Virtual Machines

**Student Name:** Joya Jones

**Date Completed:** 10/11/2026

Summarize this week's key concepts in your own words — not copy-pasted definitions.

## Key Concepts This Week

- File permissions: read/write/execute × owner/group/other, and reading `ls -l`
- Changing permissions with `chmod` (symbolic and numeric) — and THE GATEKEEPER'S RULE
- Windows ACLs, read with `Get-Acl` (the real-world `icacls` tool does the same job, but is not available in the simulator)
- Wildcards (`*`, `?`, `[ ]`) and searching inside files with `grep`/`Select-String`
- Virtual machines: host vs. guest, the hypervisor, Type 1 vs. Type 2, isolation
- The VM lifecycle: create, start, stop (deallocate), snapshot, delete — and what each costs
- Golden snapshots — how your Weeks 6–12 lab machines are made

## In My Own Words

**Decode `-rw-r-----` audience by audience: who can do what to this file?**

```
The file owner can read or change this file, the group can read, and no other users have access to read or change. No audience has execute permissions.
```

**What is a hypervisor, and what are its two jobs?**

```
A hypervisor is software that sits on top of computer hardware, allocates CPU, RAM, and storage to create distinct virtual machines, and maintains the barrier that separates machines from each other.
```

**A stopped VM still costs a little money. What is it paying for, and what's the only way to reach a true zero?**

```
A stopped VM still has disk space reserved for its operation in storage hardware, so the only way to reach a true zero for billing purposes is to permanently delete it. This frees up all storage that had been set aside.
```

---

## Submission Checklist

- [x] I summarized each concept in my own words, not copied definitions

- [x] I answered all three "In My Own Words" prompts

- [x] This file is committed to my portfolio repo at `week-04/notes.md`
