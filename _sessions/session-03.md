---
session: 3
date: 2026-10-26
title: "SGX3 Fall Training 2026 Session 3 Recap: Linux Command-Line Fundamentals & Shell Mechanics"
short_title: "Linux Command-Line Fundamentals & Shell Mechanics"
description: >-
  Core Linux shell mechanics for the Bandit Report and Command Cheat Sheet:
  SSH on non-standard ports, hidden files, filenames with spaces or leading
  dashes, and identifying file types with the OverTheWire Bandit wargame.
---
Mastering shell navigation and syntax forms the foundational core of the SGX3 curriculum. Standard scientific computing environments, supercomputers (e.g., ACCESS-CI, NAIRR, TACC), and science gateways operate almost exclusively via headless Linux shells. Participants were introduced to the command-line mechanics required for Task Sheet Item 5—the Bandit Report and Command Cheat Sheet—using the [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) wargame environment.

## Core Linux Command Cheat Sheet

| Command / Syntax | Technical Description & Research Context |
|---|---|
| `ssh -p 2220 user@host` | Connects to remote servers over non-standard SSH ports (Bandit wargame target port). |
| `cd /path/to/dir` | Changes directory; enforces strict Linux case-sensitivity rules. |
| `ls -la` | Lists all directory entries, including hidden dotfiles (`.bashrc`, `.ssh`) and permissions. |
| `cat filename` | Outputs full text content of plain ASCII files to stdout. |
| `cat "file name"`<br>`cat file\ name` | Handles spaces in file names using explicit double quotes or backslash escaping. |
| `command -- -filename` | Double dash syntax instructs CLI parsers to treat leading dashes as text, not option flags. |
| `file filename` | Analyzes file headers to distinguish plain ASCII text from raw binary executables. |
| `command *` | Wildcard expansion for pattern matching across arbitrary file series. |

## Detailed Command Mechanics

### 1. Remote SSH Connections via Non-Standard Ports

```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

Standard SSH traffic defaults to port 22. In multi-tenant HPC environments and sandboxed wargames, services are routinely mapped to non-standard ports. The `-p` flag explicitly routes the encrypted tunnel to port 2220.

### 2. Directory Inspection & Hidden File Recovery

```bash
ls -la
```

The `-l` flag renders detailed file attributes (permissions, ownership, file size, modification timestamps), while the `-a` flag reveals hidden dotfiles (files prefixed with `.`, such as hidden configuration files or hidden storage targets).

### 3. Escaping Spaces in Filenames

```bash
cat spaces\ in\ this\ filename
cat "spaces in this filename"
```

The Linux shell uses whitespace as a command argument delimiter. To process filenames containing spaces, operators must either escape each space with a backslash (`\ `) or enclose the entire path within string quotes (`""`).

### 4. Parsing Files Starting with Dashes

```bash
cat -- -file-starting-with-dash
```

When a filename begins with a hyphen (e.g., `-file`), CLI parsers misinterpret the filename as a command-line flag. Placing a double dash (`--`) signals the end of command options, forcing the parser to treat subsequent arguments strictly as positional path parameters.

### 5. Determining Data Types with `file`

```bash
file data.dat
```

File extensions in Linux are purely conventions and do not dictate file behavior. Executing `file` inspects the underlying magic bytes in the file header, allowing engineers to verify whether an unknown file contains human-readable ASCII text, compressed archives, or raw compiled binary code before executing commands like `cat`.
