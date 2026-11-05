---
session: 3
date: 2026-10-26
title: "SGX3 Fall Training 2026: Session 3 — Demystifying Linux Mechanics and OverTheWire Bandit Wargames"
short_title: "Demystifying Linux Mechanics and OverTheWire Bandit Wargames"
description: >-
  An intensive dive into Linux terminal mechanics: SSH on custom ports, file
  inspection, irregular filenames, and a peer-led walkthrough of OverTheWire
  Bandit Levels 0 through 4.
---

**Presenters:** Jeaime Powell (HPC Specialist & Workforce Development Lead), Dr. Linda Hayden (Co-PI & Workforce Development Lead), Kimora Mason (Student Assistant), Abraham Ashade (Student Mentor)

## Transitioning from Graphical UIs to Command-Line Mastery

On October 26, 2026, the SGX3 Fall Training cohort convened for Session 3, embarking on an intensive technical deep dive into Linux terminal mechanics and remote High-Performance Computing (HPC) environments. Moving away from traditional graphical user interfaces (GUIs), lead instructor Jeaime Powell and student mentor Abraham Ashade introduced trainees to the foundational command-line interface (CLI) skills required to navigate national cyberinfrastructure, manage remote server resources, and solve security puzzles.

The session centered on the **OverTheWire Bandit Wargames**, a progressive cybersecurity challenge designed to build terminal confidence through gamified problem-solving. Powell demystified the underlying mechanics of terminal interactions, explaining that while modern operating systems rely on visual folder windows, headless HPC clusters require researchers to issue explicit textual commands to list, inspect, manipulate, and transfer data files across remote servers.

## Hands-On Technical Concepts and Terminal Mechanics

The technical instruction covered critical command-line protocols and file-system behaviors:

- **Secure Shell (SSH) & Custom Port Syntax:** Trainees learned how to establish encrypted remote connections using SSH syntax. Powell highlighted the necessity of specifying non-standard server ports using the `-p` flag (e.g., `ssh -p 2220 bandit0@bandit.labs.overthewire.org`), contrasting standard web ports with customized HPC security configurations.
- **Linux Case Sensitivity & Process Control:** The team emphasized that Linux file systems treat uppercase and lowercase characters as distinct entities (e.g., `Bandit` vs. `bandit`). Additionally, instructors introduced `Ctrl+C` as an essential break sequence to terminate frozen processes or escape stuck commands without closing the terminal window.
- **Directory Navigation & File Inspection:** Trainees practiced listing directory contents using `ls` and `ls -la`, uncovering hidden dotfiles (files prefixed with `.`). They used `cat` (concatenate) to display file contents and the `file` command (`file ./*`) to inspect file types—distinguishing readable ASCII text from raw binary data.
- **Handling Complex Filenames:** Student mentor Abraham Ashade demonstrated advanced terminal tricks for handling irregular file names, including escaping spaces with backslashes (`\ `), enclosing file names in double quotes (`""`), using wildcards (`*`), and applying the double-dash (`--`) end-of-options marker to read files named with leading dashes (e.g., `-`).

## Peer-Led Mentorship and Program Milestones

Demonstrating the program's collaborative peer mentorship model, junior computer science scholar **Abraham Ashade** led the cohort through a live, step-by-step walkthrough of Bandit Levels 0 through 4. Ashade demonstrated how to extract passwords, update individual **Bandit Command Cheat Sheets**, and transition between levels by exiting current sessions (`exit`) and logging into subsequent accounts (`bandit1`, `bandit2`, `bandit3`, `bandit4`). Returning student **Dillon "Lo" Moore** supported peer troubleshooting and prepared to co-lead the upcoming Bandit training modules.

The session also welcomed new cohort participant **Charlie Nelson**, with Jeaime Powell setting up a dedicated student deliverable directory and task sheet repository. Dr. Linda Hayden addressed the cohort regarding program milestones, reminding trainees that while completing Bandit Level 25 is the mandatory task sheet requirement by December 30th, students should aim beyond the baseline—encouraging them to tackle all 33 levels of the wargames. Dr. Hayden and Powell concluded by contextualizing these technical exercises within the upcoming fall schedule, preparing students for the SGX3 NSF Site Visit (Dec 1–3), the Costa Rica Hackathon (Dec 7–11), and final GitHub Portfolio presentations scheduled for mid-December.

## Session 3 Resources and URLs

All program links are also collected on the [Resources]({{ '/resources/' | relative_url }}) page.

| Website/Resource Name | Description | URL |
|---|---|---|
| **Student Deliverables Google Drive** | Main parent directory where trainees access personal folders and upload task sheet progress and screenshots. | Shared directly with participants |
| **OverTheWire Bandit Wargames** | Official cybersecurity challenge portal used throughout the training to teach Linux commands and terminal navigation. | [overthewire.org/wargames/bandit](https://overthewire.org/wargames/bandit/) |
