# Week 2 Lab — Explore Your Own Machine (Real Specs & Live Activity)

**Student Name:** Joya Jones

**Date Completed:** 9/27/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 2  
**Submission Path:** `week-02/labs/lab-02-machine-exploration.md`

---

## Overview

Lab 01 got you diagramming how hardware, OS, and software interact — in theory. This lab makes it real, in one sitting. First, you'll look up your own machine's actual specs (OS version, RAM, storage) using its built-in settings screens. Then you'll open Task Manager (Windows) or Activity Monitor (Mac) and watch those same hardware and software layers working together live — CPU usage, memory usage, and real running processes — and connect what you see back to your Lab 01 diagram.

**No terminal or command line is required this week** — that starts in Week 3. Settings screens, Task Manager, and Activity Monitor are all point-and-click tools.

---

## Lab Environment

| Component | Details |
|---|---|
| Environment | Your own computer (Windows or Mac) — no VM, no cloud, no install needed |
| Required Materials | Your computer's built-in Settings/About screen; Task Manager (Windows: `Ctrl+Shift+Esc`) or Activity Monitor (Mac: `Cmd+Space`, then type "Activity Monitor") |

**Prerequisite:** Lab 01 completed — you'll reference your diagram in this lab's Analysis Questions.

---

## Part A — Find Your Real Specs

**Before you start:** here's what to expect so you don't second-guess yourself. On Windows, you're looking for a page titled **About**, reached via **Settings → System → About**, listing your device specs under "Device specifications." On Mac, you're looking for a window titled **About This Mac** (click the Apple menu, top-left corner), with an Overview tab listing your chip, memory, and macOS version. If what's on your screen doesn't roughly match that, you're in the wrong menu — try again before recording anything below.

### Step 1 — Find Your OS Version

Open your computer's system settings (Windows: **Settings → System → About**. Mac: **Apple menu → About This Mac**) and find the exact operating system name and version you're running.

**OS and version:** Windows 11 Pro, version 25H2

```
(e.g., "Windows 11, version 23H2" or "macOS Sonoma 14.4")
```

### Step 2 — Check Your Installed RAM

On the same settings screen, find how much RAM (memory) is installed on your computer.

**Installed RAM:** 32 GB

```
32 GB
```

### Step 3 — Check Your Available Storage

Find your computer's total storage capacity and how much is currently free (Windows: **Settings → System → Storage**. Mac: **About This Mac → Storage**).

**Total storage:** 954 GB

```
954 GB
```

**Free storage:** 468 GB

```
468 GB
```

---

## Part B — Watch It Live

Your Part A numbers are a snapshot. This part shows those same layers actually working, moment to moment.

### Step 1 — Open Task Manager or Activity Monitor

Windows: press `Ctrl+Shift+Esc`. Mac: press `Cmd+Space`, type "Activity Monitor," and press Enter.

### Step 2 — Find the Performance / CPU Tab

Windows: click the **Performance** tab. Mac: click the **CPU** tab.

### Step 3 — Freeze the List Before You Read It

The process list updates constantly and can be hard to read while it's jumping around. Before recording anything, click the **Name** column header (or **Memory**, if you'd rather sort by what's using the most RAM) to sort the list — this won't stop it from updating, but it keeps things from reordering under you while you read.

### Step 4 — Record CPU Usage

Look at the current CPU usage percentage.

```
Current CPU usage: ____%
```

### Step 5 — Record Memory Usage

Find how much RAM is currently in use, out of your total installed RAM (the same total you looked up in Part A).

```
RAM in use: ____   out of total: ____
```

### Step 6 — List Five Running Processes

List five processes running right now. For each, write your best guess at what it is or does — you don't need to be 100% correct, just reason it out. If you spot something on the cheat sheet below, you can use that, but try at least a couple you don't recognize.

**Cheat sheet — common processes you'll likely see (not exhaustive, just a starting reference):** 1. Process name: SupportAssistAgent     What I think it does: Dell computer helper application 2. Process name: Antimalware Service Executable      What I think it does: "Windows Defender scanning files in the background" 3. Process name: WebView2 Manager       What I think it does: related to the Zoom app that runs in the background on my computer 4. Process name: Spotify Launcher      What I think it does: launches and manages Spotify music app 5. Process name: NVIDIA Container      What I think it does: supports processes that use the graphics card

| Process Name | Usually Seen On | What It Generally Is |
|---|---|---|
| explorer.exe | Windows | The Windows desktop and file browser itself — normal, always running |
| svchost.exe | Windows | A generic host for background Windows services — several running at once is normal |
| Antimalware Service Executable | Windows | Windows Defender scanning files in the background — normal |
| dwm.exe | Windows | Desktop Window Manager — handles visual effects like transparency and window animations |
| System Idle Process | Windows | Not a real program — represents how much CPU is doing *nothing* right now |
| WindowServer | Mac | Manages everything drawn on your screen — always running |
| Finder | Mac | The Mac desktop and file browser itself — normal, always running |
| mdworker / mds | Mac | Spotlight's background indexing service — normal, can spike briefly after installing apps |
| launchd | Mac | The very first process Mac starts — manages and launches other background services |

```
1. Process name: __________   What I think it does: __________
2. Process name: __________   What I think it does: __________
3. Process name: __________   What I think it does: __________
4. Process name: __________   What I think it does: __________
5. Process name: __________   What I think it does: __________
```

### Step 7 — Screenshot and Embed

Take a screenshot of Task Manager or Activity Monitor showing your CPU/memory usage and process list.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-02/`.
2. Click **Add file → Upload files**, then drag in your screenshot, and give it a descriptive name (lowercase, hyphens, no spaces — e.g. `machine-exploration.png`).
3. Scroll down and click **Commit changes**.
4. Click on the uploaded image's filename to open it — you'll see the image itself displayed on the page.
5. Right-click directly on the image and choose **Copy image address** (Chrome/Edge) or **Copy Image Link** (Firefox).
6. Come back to this file, open the pencil (edit) icon, and paste that link into the embed line below, in place of the placeholder:

![Task Manager / Activity Monitor screenshot](https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/refs/heads/main/assets/screenshots/week-02/machine-exploration.png)

**If right-click doesn't show that option:** click the small download-arrow icon in the top-right of the image preview instead, then copy the URL from your browser's address bar.

**My Screenshot:** https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/refs/heads/main/assets/screenshots/week-02/machine-exploration.png

### Step 8 — Connect the Numbers

In your own words, explain how the real numbers you found in Part A (OS version, RAM, storage) relate to what you just watched live in Part B. Which number describes hardware, and which describes the OS?

```
Windows 11 Pro, version 25H2 describes the operating system, while 32 GB of RAM and 954 GB of storage describe the hardware installed in my computer. In Task Manager, 58% memory describes the percentage of my RAM currently in use by active processes, and 4% CPU usage represents how much of the processor's capacity is being used at that moment. Although those percentages refer to hardware resources, they also show the operating system at work because Windows is responsible for allocating and coordinating those resources across processes.
```

---

## Analysis Questions

### Analysis Question 1

Pick one process from your list in Part B, Step 6. Is it "software" in the sense Lab 01 used that word? Explain how it depends on the OS and on hardware to actually run.

```
The process Spotify Launcher seems to involve a group of 11 related processes in this case, and would be considered software, as represented in Lab 01. It depends on Windows to actually make it run by starting and managing the necessary processes, then allocating the hardware resources it needs. The CPU executes its instructions, RAM provides the active working space, and storage holds the program and its data long-term. Spotify Launcher was using about 380.5 MB of memory at the time captured, even though, with music not playing, the CPU usage was 0%.
```

### Analysis Question 2

Your CPU usage number changes constantly, even when you're not doing anything. Explain, in your own words, why watching this number matters for security work — not just for performance. (Hint: think about what it might mean if a process you don't recognize suddenly spikes CPU usage.)

```
CPU usage shows how much processing work the OS has allocated for the machine to do at a given time, and which processes represent that work being done. For security purposes, an unexpected spike can be a useful clue, especially if it comes from a process I do not recognize or was not expecting to be active. Something caused that process to start up or to begin doing more work than usual. A sudden increase would not automatically mean the process is malicious, as there are many subprocesses of familiar programs that could be triggered for any number of reasons, but it could give me as a cybersecurity professional a reason to investigate further. I would want to figure out what the process was doing, where it came from, and whether it should be removed from the system.
```

### Analysis Question 3

Compare what you saw in Task Manager/Activity Monitor to the diagram you built in Lab 01. What's the same? What did watching your machine live show you that a static diagram couldn't?

```
Processes listed in Task Manager reflected the same relationship I diagrammed in Lab 01: software running through the operating system and using hardware resources of CPU and RAM. Task Manager showed the real-time allocation of CPU resources across multiple forms of software, as well as how much active memory space was being used by each. The static diagram could not show that this resource usage is constantly changing even without user interaction, or that a process may still be taking up space in RAM even when it has no active CPU involvement at that moment.
```

---

## Submission Checklist

- [x] OS version, installed RAM, and total/free storage looked up and recorded (Part A)

- [x] Task Manager or Activity Monitor opened and list sorted before recording (Part B)

- [x] Current CPU usage recorded

- [x] Current RAM usage recorded, alongside total RAM from Part A

- [x] Five running processes listed, each with a reasoned guess at what it does

- [x] Screenshot uploaded to `assets/screenshots/week-02/` and embedded using a copied image link

- [x] Connection explanation written (Part B, Step 8 — minimum 2 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [ ] This file is committed to your portfolio repo at `week-02/labs/lab-02-machine-exploration.md`

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
