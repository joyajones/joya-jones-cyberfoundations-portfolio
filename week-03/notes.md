# Week 3 Notes — Windows, Linux, and Your First Commands

**Student Name:** Joya Jones

**Date Completed:** 10/4/2026

Summarize this week's key concepts in your own words — not copy-pasted definitions.

## Key Concepts This Week

- Files, folders, and the file-system tree
- Windows vs. Linux file system differences (paths, case-sensitivity, drives)
- Navigating the shell: `pwd`/`Get-Location`, `ls`/`dir`, `cd`
- Reading files and getting help: `cat`/`type`, `--help`/`man`/`Get-Help`
- Creating and organizing: `mkdir`/`touch`, `cp`/`mv`, `rm`

## In My Own Words

**What's the difference between a file and a folder, and how do they form a tree together?**

```
A file is a single item that is stored as one unit in the computer system, and a folder (or directory) is a container that can hold both files and other folders. From the single root of a Linux system, or the multiple lettered Drive roots of a Windows system, folders serve as the "branches" of that tree, and files are the "leaves" at the end of those branches. Together, the root, branches, and leaves represent the machine's hierarchy of information.
```

**How does a Windows-style file path differ from a Linux-style file path?**

```
A Windows-style path uses drive letters, backslashes, and is not case-sensitive. 'C:\Users\Ivy\Reports\report-a' will take you to the same place as 'C:\Users\Ivy\reports\Report-A'. Linux-style paths all stem from one root folder, represented by a single forward slash, only use forward slashes, and are case-sensitive. 'home/ivy/reports/report-A' is a different file and in a different folder from 'home/ivy/Reports/report-a'.
```

**One command from this week you feel most confident with — and why?**

```
I feel most confident with the command that allows me to look around and see what files and folders are in my location: 'ls' 'dir' 'Get-ChildItem'. So far, I've found it more useful and meaningful to know what is in my immediate vicinity than the name of the folder I am in. Of course both are important, but one helps me feel more grounded.
```

---

## Submission Checklist

- [x] I summarized each concept in my own words, not copied definitions

- [x] I answered all three "In My Own Words" prompts

- [x] This file is committed to my portfolio repo at `week-03/notes.md`
