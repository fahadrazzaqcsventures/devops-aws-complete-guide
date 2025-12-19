# File and Directory Management (Theory)

## Purpose

This document explains **how Linux organizes files and directories and how engineers manipulate them efficiently**. Mastery of file and directory management is critical for DevOps, SREs, and Cloud engineers because **all automation, troubleshooting, and application deployment involve interacting with files and directories**.

This is theory-first: *why* things exist and *how* Linux approaches file management.

---

## Linux Filesystem Principles

Linux organizes files in a **single-root hierarchy**:

* Everything starts at `/` (root)
* Devices, configuration, logs, and user data are all represented as files
* Drives are mounted as directories — no drive letters

> **Design principle:** "Everything is a file"

### Files vs Directories

* **File:** Stores data (text, binaries, configs)
* **Directory:** Maps names to inodes (lookup table)

> Directories are not containers; they are **indexes** to files and subdirectories.

### Hidden Files

* Begin with `.`
* Used for configuration and shell behavior
* Examples: `.bashrc`, `.ssh/`

### Symbolic vs Hard Links

* **Symbolic link:** Pointer to another path
* **Hard link:** Another name for the same inode

> In DevOps, symlinks are commonly used for configs, releases, and mount points.

---

## Core Directories

| Directory | Purpose                   | Production Relevance          |
| --------- | ------------------------- | ----------------------------- |
| `/`       | Root of filesystem        | Starting point for everything |
| `/bin`    | Essential binaries        | `ls`, `cp`, `mv`, `cat`       |
| `/sbin`   | System/admin binaries     | Recovery, maintenance         |
| `/etc`    | Configuration files       | Services, networking, users   |
| `/var`    | Variable data             | Logs, caches, spools          |
| `/home`   | User home directories     | Developers and service users  |
| `/tmp`    | Temporary files           | Cleared on reboot             |
| `/opt`    | Optional software         | Vendor apps, agents           |
| `/usr`    | User programs & libraries | Installed packages            |
| `/proc`   | Process & kernel info     | Live system inspection        |
| `/dev`    | Device files              | Disks, terminals, mounts      |

---

## Absolute vs Relative Paths

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

> Best practice: Automation scripts should prefer **absolute paths**.

---

## Basic Commands Conceptual Overview

| Command | Purpose                  |
| ------- | ------------------------ |
| `pwd`   | Print current directory  |
| `ls`    | List directory contents  |
| `cd`    | Change directory         |
| `touch` | Create/update file       |
| `mkdir` | Create directory         |
| `cp`    | Copy files/directories   |
| `mv`    | Move or rename           |
| `rm`    | Remove files/directories |
| `stat`  | View file metadata       |

Flags & Tips:

* `ls -l` → show permissions and ownership
* `ls -a` → show hidden files
* `ls -h` → human-readable sizes
* `mkdir -p a/b/c` → create nested directories
* `cp -r dir1 dir2` → recursive copy of directories
* `rm -rf dir` → delete a directory tree (use with caution)
* `rmdir emptydir` → remove an empty directory

---

## Why This Matters in DevOps

* Inspecting logs and configs
* Mounting volumes for Docker and Kubernetes
* Automating scripts for deployment
* Recovering broken systems

> If you cannot navigate and manipulate files confidently, you cannot operate Linux in production.

---

## Next Step

Proceed to the [**Linux File & Directory Management – Practical Lab**](../../../98-home-lab/labs/01-linux/03-file-and-directory-management/README.md).
