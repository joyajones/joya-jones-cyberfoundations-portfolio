# Week 2 Lab — Cybersecurity Landscape & Digital Infrastructure Overview

**Student Name:** Joya Jones

**Date Completed:** 9/27/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 2  
**Submission Path:** `week-02/labs/lab-01-hardware-os-software-diagram.md`

---

## Overview

In this lab, you build a working mental model of the system you'll be securing throughout this course: the hardware, operating system, and software layers that make up every computer, and where the cybersecurity field fits around them. This lab has two parts. Part A connects this week's material to the CyberFoundations City map. Part B has you build and explain a diagram of how a computer's hardware, OS, and software layers interact.

**No terminal or command line is required this week** — that starts in Week 3.

---

## Lab Environment

| Component | Details |
|---|---|
| Environment | Browser-based Lab Portal (Module 1 orientation) |
| Required Materials | CyberFoundations City map; a diagram tool of your choice (hand-drawn and photographed, or any digital tool) |

**Prerequisite:** Portfolio repo created from the CyberFoundations student template in Week 1. This file is already in your repo at `week-02/labs/lab-01-hardware-os-software-diagram.md`, ready to fill in.

**New to the Lab Portal?** Watch this short walkthrough of how to find your Week 2 lab worksheet: [Accessing the Lab Worksheet — Step by Step](PASTE-VIDEO-LINK-HERE) *(~3 min)*.

---

## Part A — CyberFoundations City & the Cybersecurity Landscape

The CyberFoundations City map is your visual guide to the next 11 weeks. Each district represents a module of this course. This part connects this week's material to the map you were introduced to in Week 1.

### Step 1 — Open the Lab Portal Orientation Module

Log into the Lab Portal with your Microsoft account. From your Student Dashboard, open the **Module 1 orientation** module.

### Step 2 — Complete the Orientation Walkthrough

Work through the orientation content. It covers the same hardware/OS/software material as this week's lessons from a different angle — use it to check your understanding, not to replace the lessons.

### Step 3 — Locate This Week's District on the City Map

Open the CyberFoundations City map (introduced in Week 1, Lesson 6). Identify which district corresponds to Module 1 — Digital Infrastructure & CLI.

**District name:** The Foundry District

```
The Foundry District
```

**Why this district fits this week's topics (1–2 sentences):** A foundry is traditionally a factory where metals are melted and poured into molds to make custom components, which is a foundational step in manufacturing. This week's topics reveal the foundational components of digital systems, which are the physical hardware and enabling operating system and software layers that we are learning to secure.

```
A foundry is traditionally a factory where metals are melted and poured into molds to make custom components, which is a foundational step in manufacturing. This week's topics reveal the foundational components of digital systems, which are the physical hardware and enabling operating system and software layers that we are learning to secure.
```

---

## Part B — Hardware, OS, and Software Diagram

A computer is a stack of layers: physical hardware at the bottom, an operating system managing that hardware in the middle, and the software you actually use on top. This part has you draw that stack and explain it in your own words.

### Step 1 — Identify the Layers

Before drawing anything, list the three layers you'll diagram and one example of what lives at each layer.

**Hardware layer — one example component:** CPU

```
(e.g., CPU, RAM, storage — your choice)
```

**Operating system layer — name an OS:** Windows

```
(e.g., Windows, Linux, macOS)
```

**Software layer — one example application:** Google Chrome

```
(e.g., a web browser, a word processor)
```

### Step 2 — Sketch Your Diagram

Sketch a simple diagram (hand-drawn and photographed, or built in any digital tool) showing how the hardware, OS, and software layers stack and interact. Arrows or labels showing "what talks to what" matter more than visual polish. If you'd like a free browser-based option instead of hand-drawing, try [draw.io](https://www.drawio.com/) — no account required to get started.

### Step 3 — Upload and Embed Your Diagram

Upload your diagram image directly into your repo's assets folder — keep it there rather than pasting it loose into this file, so all of this week's images stay together and organized.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-02/`.
2. Click **Add file → Upload files**, then drag in your diagram image, and give it a descriptive name (lowercase, hyphens, no spaces, no timestamps — e.g. `hardware-os-software-diagram.png`).
3. Scroll down and click **Commit changes**.
4. Click on the uploaded image's filename to open it — you'll see the image itself displayed on the page.
5. Right-click directly on the image and choose **Copy image address** (Chrome/Edge) or **Copy Image Link** (Firefox).
6. Come back to this file, open the pencil (edit) icon, and paste that link into the embed line below, in place of the placeholder:

![Hardware/OS/software diagram](https://raw.githubusercontent.com/joyajones/joya-jones-cyberfoundations-portfolio/refs/heads/main/assets/screenshots/week-02/hardware-os-software-diagram.png)

**If right-click doesn't show that option:** click the small download-arrow icon in the top-right of the image preview instead, then copy the URL from your browser's address bar.

**My Diagram:** Hardware-OS-Software

### Step 4 — Explain Your Diagram

In your own words — not a copied definition — explain how the three layers interact. Reference your own diagram directly.

```
In my diagram, the software layer (Google Chrome) sits on top of the operating system (Windows), and the operating system sits between the software and the hardware. To open Chrome, I click on the icon in the GUI provided by the OS. That click serves as a request that I, the user, am making at the "front desk." The OS then has the task of making the program available to me by starting a process, which it does by recruiting hardware resources: CPU clock time and processing capacity, and by pulling the program itself from storage into RAM, the computer's short-term or active working memory, so the work can happen while I am engaging with it. In the hardware layer of my diagram, the motherboard physically connects the CPU, RAM, and storage so those components can work together, while the lines between the OS and motherboard show the OS coordinating those hardware resources on behalf of the software.
```

---

## Analysis Questions

Answer each question in your own words. These questions connect what you did in Parts A and B to the bigger picture of this course.

### Analysis Question 1

If the operating system crashed on the computer you diagrammed, which layer(s) would stop working, and which (if any) would keep working? Explain your reasoning.

```
If the operating system in the diagram above crashed, nothing physical would happen to the hardware layer, but the software layer would become inaccessible to the user. Depending on the type of OS failure, there may be no GUI presented to provide user interactivity, or the GUI might be visible but not functional. While programs and files would still be safely held in storage, and the CPU and RAM would still be physically capable of functioning, they would lie inert without the OS to manage and coordinate them.
```

### Analysis Question 2

Pick one piece of software you use daily. Trace it down through the OS to the hardware it ultimately depends on. What would happen to that software if the hardware layer failed?

```
I chronically check my email in the Gmail app on my iPhone 15 Plus. My phone currently runs iOS version 26.4. After locating my model number, A2847, I was able to determine the specific hardware inside: a 6-core CPU, 6GB of RAM, and 128GB of storage, all connected through the phone's physical logic board (Apple's terminology for "motherboard"). The Gmail app depends on iOS to manage those hardware resources while I use it: the CPU executes instructions, RAM provides active working space, and storage holds the app and data long-term. If the hardware layer failed completely, I would no longer have a functioning device that could run iOS, much less Gmail.
```

### Analysis Question 3

Explain, in your own words, why a cybersecurity professional needs to understand all three layers — hardware, OS, and software — rather than just the software layer where most visible attacks (like phishing emails) happen.

```
A cybersecurity professional should be prepared and skilled enough to protect every area of a digital system's attack surface. Threat actors can gain access at all three layers, and each layer also has its own affiliated vulnerabilities. Because the hardware, operating system, and software all depend on one another, a weakness in one layer can affect the security of the others. The deeper the understanding of the infrastructure that attackers are trying to control, the better the cybersecurity professional can anticipate and respond to attacks.
```

---

## Lab Report Questions

Answer each question in complete sentences.

**1. What is the cybersecurity landscape, and why does it matter to someone starting this course?**

```
The cybersecurity landscape is the full, big picture of who is building and protecting digital systems, who is attacking them, and how they are constantly adapting to one another. Someone starting this course intends to fulfill the role of protector, and the first step in doing so is to learn the entire scope of what they will be responsible for securing. With a limited understanding of the landscape, they can actually contribute to a system’s weaknesses, or vulnerabilities, by not having the capacity or know-how to block, detect, or investigate all possible threats in their environment.
```

**2. Which CyberFoundations City district did you identify in Part A, and how does its theme connect to the hardware/OS/software material in Part B?**

```
The Foundry District of CyberFoundations City corresponds to digital infrastructure and the command line interface (CLI). Its theme connects to Part B because the hardware, operating system, and software layers I diagrammed are the foundational components that work together to make a computer usable, which is what digital infrastructure is built on.
```

**3. Of the three layers (hardware, OS, software), which one do you think is hardest to secure, and why?**

```
Of the three layers, I think the software layer is the hardest to secure. Innumerable apps mean myriad openings for attackers to gain entry, and this is also the layer most exposed to everyday user error. Even when vulnerabilities are found and fixed, users are still required to take action in the form of software updates, which many are either resistant to doing or do not understand the importance of. 
```

---

## Submission Checklist

- [x] Lab Portal Module 1 orientation completed

- [x] District identified and explained

- [x] Hardware, OS, and software layer examples listed

- [x] Diagram uploaded to `assets/screenshots/week-02/` and embedded using a copied image link (not pasted loose, not a local file path)

- [x] Diagram explanation written in your own words (minimum 3 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] All three Lab Report Questions answered in complete sentences

- [ ] This file is committed to your portfolio repo at `week-02/labs/lab-01-hardware-os-software-diagram.md`
