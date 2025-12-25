# Linux Fundamentals: Services, Scheduling, and systemd (Theory)

## Purpose

This document explains **how Linux manages long‑running services and scheduled tasks** using `systemd`, `cron`, and one‑time job schedulers.

For DevOps and SRE engineers, this knowledge is critical because **availability, startup order, automation, and recovery** are controlled here. Most production outages ultimately involve a service that failed to start, restart, or schedule correctly.

This is theory‑first: *how the system thinks*.

---

## What Is a Service?

A **service** is a long‑running background process (daemon) that provides functionality such as:

* Web servers (nginx)
* Databases (mysql, postgres)
* Monitoring agents
* CI/CD runners

Services must:

* Start reliably
* Restart on failure
* Integrate with system boot
* Expose logs and status

---

## systemd Overview

`systemd` is the **init system** and service manager on modern Linux.

Key characteristics:

* First user‑space process (PID 1)
* Parallel service startup
* Dependency management
* Integrated logging (journald)

> systemd replaces legacy init systems like SysVinit and Upstart.

---

## Units in systemd

systemd manages resources called **units**.

Common unit types:

| Unit Type  | Purpose                           |
| ---------- | --------------------------------- |
| `.service` | Service processes                 |
| `.target`  | Logical groupings (runlevels)     |
| `.timer`   | Scheduled jobs (cron alternative) |
| `.mount`   | Mount points                      |

In practice, DevOps engineers primarily interact with **service units**.

---

## Service Lifecycle Concepts

A service has two independent states:

### Runtime State

* Started
* Stopped
* Restarted

Controlled by:

* `systemctl start`
* `systemctl stop`
* `systemctl restart`

### Boot State

* Enabled (starts at boot)
* Disabled (manual only)

Controlled by:

* `systemctl enable`
* `systemctl disable`

> Starting a service does **not** mean it will start on reboot.

---

## Service Status and Health

`systemctl status` provides:

* Active state
* Exit codes
* Restart attempts
* Recent logs

This is the **first command** used in production incidents.

---

## Legacy Service Management

Older systems used the `service` command.

It still exists for compatibility:

* `service nginx start`
* `service nginx status`

Internally, this is a wrapper around systemd.

> Use `systemctl` for all modern automation and troubleshooting.

---

## Scheduling Concepts

Linux provides **three scheduling models**:

### 1. Cron (Recurring Jobs)

Used for:

* Backups
* Log rotation
* Periodic cleanup

Cron jobs:

* Run at fixed times
* Are stateless
* Do not survive missed runs

---

### 2. at / batch (One‑Time Jobs)

* `at` → run once at a specific time
* `batch` → run when system load is low

Used for:

* Deferred maintenance
* Off‑peak processing

---

### 3. systemd Timers (Modern Alternative)

systemd timers:

* Replace cron in modern systems
* Support dependencies
* Integrated logging

Common in enterprise environments.

---

## Sleep and Delays

`sleep` introduces execution delays.

Used in:

* Scripts
* CI/CD pipelines
* Startup sequencing

Delays are **coordination tools**, not scheduling systems.

---

## Why This Matters in DevOps

You will use service and scheduling control when:

* Debugging failed deployments
* Ensuring services survive reboots
* Scheduling backups and jobs
* Managing CI/CD runners
* Operating Kubernetes nodes

If you cannot control services and schedules, you cannot guarantee reliability.

---

## Key Takeaway

> systemd controls **when things start, stop, and recover**.
> Scheduling controls **when work happens**.

Mastery here separates operators from button‑clickers.

---

## Next Step

Proceed to [**Services, Scheduling, and systemd – Hands‑On Lab**](../../../labs/01-linux/14-services-scheduling-and-systemd/README.md) to build operational confidence.
