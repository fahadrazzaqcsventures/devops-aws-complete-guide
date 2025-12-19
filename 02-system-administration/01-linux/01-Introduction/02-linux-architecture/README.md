# Linux Architecture

## Purpose

This document explains **how Linux is architected internally** and how its major components interact in a production system.

Understanding Linux architecture is critical for DevOps and SRE work because performance issues, outages, and security incidents almost always trace back to **kernel behavior, resource isolation, or user‑space services**.

---

## High-Level Linux Architecture

At a high level, Linux is divided into two major domains:

```
+---------------------------+
|        Applications       |
+---------------------------+
|        User Space         |
+---------------------------+
|           Kernel          |
+---------------------------+
|          Hardware         |
+---------------------------+
```

This separation enforces **stability, security, and isolation**.

---

## Hardware Layer

The hardware layer includes:

* CPU
* RAM
* Storage devices
* Network interfaces

Linux does not allow applications to interact with hardware directly. All access is mediated by the kernel.

Production relevance:

* CPU saturation
* Disk I/O bottlenecks
* Network throughput limits

---

## Kernel Layer

The **Linux kernel** is the core of the operating system. It runs in **kernel mode** with full privileges.

### Kernel Responsibilities

#### 1. Process Scheduling

* Decides which process runs on which CPU
* Handles multitasking and priorities

Impacts:

* Application latency
* Load behavior

---

#### 2. Memory Management

* Allocates and frees RAM
* Implements virtual memory
* Handles swapping and OOM conditions

Impacts:

* Application crashes
* Performance degradation

---

#### 3. Filesystem Management

* Manages filesystems (ext4, xfs, etc.)
* Handles permissions and inodes

Impacts:

* Data integrity
* Disk usage incidents

---

#### 4. Device Drivers

* Controls hardware via drivers
* Abstracts devices as files

Examples:

* `/dev/sda`
* `/dev/null`

---

#### 5. Networking Stack

* Implements TCP/IP
* Manages ports and sockets

Impacts:

* Service connectivity
* Packet loss

---

## User Space

User space is where **applications and services run with restricted privileges**.

Components include:

* Shells (bash, sh)
* System utilities
* Daemons and services
* User applications

User-space programs must request kernel services via **system calls**.

---

## System Libraries

System libraries:

* Provide standard APIs
* Translate application requests into system calls

Example:

* `glibc`

Applications rarely invoke system calls directly.

---

## Init System

The init system is the **first user-space process** (PID 1).

Modern Linux uses **systemd**.

Responsibilities:

* Start services
* Manage dependencies
* Handle service restarts

Production relevance:

* Service failures
* Boot issues

---

## Filesystem Hierarchy

Linux uses a unified filesystem rooted at `/`.

Key directories:

* `/etc` → configuration
* `/var` → logs and variable data
* `/bin`, `/usr/bin` → binaries
* `/home` → user data

This hierarchy is part of Linux architecture, not convenience.

---

## User vs Kernel Mode

| Mode        | Description          |
| ----------- | -------------------- |
| User mode   | Limited access       |
| Kernel mode | Full hardware access |

Mode separation prevents a single application failure from crashing the system.

---

## Why Architecture Knowledge Matters in DevOps

Linux architecture knowledge enables you to:

* Diagnose performance issues
* Understand container behavior
* Troubleshoot Kubernetes nodes
* Secure systems correctly

Without this understanding, engineers rely on guesswork.

---

## Key Takeaway

> Linux is not a black box.
> It is a layered system designed for control, isolation, and reliability.

Mastering Linux means understanding how these layers interact under pressure.
