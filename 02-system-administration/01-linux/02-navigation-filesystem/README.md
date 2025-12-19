# Navigation & Filesystem (Theory)

## Purpose

This document explains **how Linux organizes data and how engineers navigate it efficiently**. Mastery of the filesystem is non-negotiable for DevOps, SRE, and Cloud engineers because every production issue eventually requires interacting with files, logs, binaries, and configuration.

This is theory-first: *why* things exist and *how* Linux thinks.

---

## The Linux Filesystem Philosophy

Linux follows a **single-root hierarchy**.

* Everything starts at `/` (root)
* Devices, configuration, logs, and user data are all represented as files
* There are no drive letters (unlike Windows)

> **Design principle:** "Everything is a file"

---

## Core Directories You Must Know

| Directory | Purpose                   | Production Relevance          |
| --------- | ------------------------- | ----------------------------- |
| `/`       | Root of filesystem        | Starting point for everything |
| `/bin`    | Essential user binaries   | `ls`, `cp`, `mv`, `cat`       |
| `/sbin`   | System/admin binaries     | Used by root for recovery     |
| `/etc`    | Configuration files       | Services, networking, users   |
| `/var`    | Variable data             | Logs, cache, spool            |
| `/home`   | User home directories     | Developer and service users   |
| `/tmp`    | Temporary files           | Cleared on reboot             |
| `/opt`    | Optional software         | Vendor apps, agents           |
| `/usr`    | User programs & libraries | Most installed packages       |
| `/proc`   | Process & kernel info     | Live system inspection        |
| `/dev`    | Device files              | Disks, terminals, mounts      |

---

## Paths: Absolute vs Relative

### Absolute Path

* Starts from `/`
* Works from any location

Example:

```bash
/etc/nginx/nginx.conf
```

### Relative Path

* Starts from current directory

Example:

```bash
./logs/app.log
```

**Rule in production:** Scripts and automation should prefer **absolute paths**.

---

## Navigation Commands (Conceptual)

| Command | Purpose                 |
| ------- | ----------------------- |
| `pwd`   | Show current directory  |
| `ls`    | List directory contents |
| `cd`    | Change directory        |

Important flags:

* `ls -l` → permissions, ownership
* `ls -a` → hidden files
* `ls -h` → human-readable sizes

---

## Files vs Directories

* **File:** Stores data (text, binary, config)
* **Directory:** Index mapping names → inodes

Key idea:

> A directory is not a container — it is a **lookup table**.

---

## Hidden Files

* Start with `.`
* Used for configuration and system behavior

Examples:

* `.bashrc`
* `.ssh/`

Hidden does **not** mean secure.

---

## Symbolic Links vs Hard Links

* **Symbolic link:** Pointer to another path
* **Hard link:** Another name for the same inode

In DevOps:

* Symlinks are common for configs and releases
* Hard links are rarely used intentionally

---

## Why This Matters in DevOps

You will use filesystem navigation when:

* Debugging containers
* Inspecting logs
* Editing configs
* Writing automation
* Mounting volumes
* Recovering broken systems

If you cannot move confidently through the filesystem, you cannot operate Linux in production.

---

## Next Step

Proceed to the [**Linux Navigation & Filesystem – Practical Lab**](../../../98-home-lab/labs/01-linux/02-navigation-filesystem/README.md):

