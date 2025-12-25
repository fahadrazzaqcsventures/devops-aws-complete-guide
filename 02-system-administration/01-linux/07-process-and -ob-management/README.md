# Processes & Jobs (Theory)

## Purpose

This document explains **how Linux executes, schedules, and controls processes** and how engineers manage foreground/background jobs in real systems.

Process control is core DevOps knowledge. Every outage, performance issue, or stuck deployment eventually requires understanding **what is running, why it is running, and how to control it safely**.

This is theory-first: *how Linux thinks about work*.

---

## What Is a Process

A **process** is a running instance of a program.

Key facts:

* Every process has a **PID** (Process ID)
* Processes are created via `fork()` and `exec()`
* Processes consume CPU, memory, file descriptors, and other kernel resources

> Linux does not run “applications” — it runs **processes**.

---

## Process Hierarchy

Linux processes form a **tree**:

* Every process has a parent (PPID)
* Orphaned processes are adopted by PID 1 (`systemd`)

This hierarchy matters for:

* Service supervision
* Container runtimes
* Zombie and orphan cleanup

---

## Process States

Common states:

| State | Meaning                              |
| ----- | ------------------------------------ |
| R     | Running or runnable                  |
| S     | Sleeping (waiting for I/O)           |
| D     | Uninterruptible sleep (disk/network) |
| Z     | Zombie (exited, not reaped)          |
| T     | Stopped (signal or debugger)         |

Persistent **D** or **Z** states are production red flags.

---

## Viewing Processes

### `ps`

`ps aux` provides a **snapshot** of all running processes.

Production usage:

* Identify high CPU or memory consumers
* Inspect command arguments
* Verify services actually started

---

### `top` and `htop`

* `top` → real-time, built-in
* `htop` → enhanced (if installed)

Used for:

* Live performance diagnosis
* Spotting runaway processes
* Observing load under traffic

---

## Signals and Process Control

Linux controls processes using **signals**.

Common signals:

| Signal       | Purpose                  |
| ------------ | ------------------------ |
| SIGTERM (15) | Graceful termination     |
| SIGKILL (9)  | Force kill (last resort) |
| SIGSTOP      | Pause execution          |
| SIGCONT      | Resume execution         |

Commands:

* `kill PID`
* `pkill name`
* `killall name`

> Always attempt graceful termination before force killing.

---

## Process Priority (Nice Values)

Linux uses **scheduler priorities**.

* Nice range: `-20` (highest) to `19` (lowest)
* Default nice value: `0`

Commands:

* `nice -n 10 cmd`
* `renice -n 10 -p PID`

Production relevance:

* Prevent batch jobs from starving services
* Control CI runners, backups, and cron jobs

---

## Jobs vs Processes

A **job** is a shell concept.

* Jobs exist only within a shell session
* Processes exist system-wide

Job control allows:

* Foreground execution
* Background execution
* Suspension and resumption

---

## Job Control Commands

| Command | Purpose                  |
| ------- | ------------------------ |
| `jobs`  | List shell jobs          |
| `bg`    | Resume job in background |
| `fg`    | Bring job to foreground  |
| `nohup` | Detach from terminal     |

Used heavily in:

* SSH sessions
* Ad-hoc debugging
* Long-running scripts

---

## Timing and Monitoring

* `time command` → measure execution time
* `watch -n 1 cmd` → rerun command at intervals

Production examples:

* Timing deployments
* Monitoring memory usage live
* Observing metric changes

---

## Why This Matters in DevOps

Process control enables you to:

* Debug stuck deployments
* Kill runaway services safely
* Tune system performance
* Operate containers and nodes
* Understand Kubernetes behavior at the node level

Without process literacy, automation becomes dangerous.

---

## Next Step

Proceed to [**Processes & Jobs – Hands-On Lab**](../../../98-home-lab/labs/01-linux/07-process-and%20-ob-management/README.md) to build operational confidence.
