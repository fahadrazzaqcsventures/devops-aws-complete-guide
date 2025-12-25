# System Information & Logs (Theory)

## Purpose

This document explains **how to inspect system state, hardware, performance, and logs** on a Linux system. This knowledge is mandatory for DevOps and SRE roles because **every incident begins with understanding what the system is doing right now and what it did before**.

This is theory-first: *what signals exist, where they come from, and how to interpret them without guessing*.

---

## System Information vs Observability

Linux exposes system state through:

* Kernel interfaces (`/proc`, `/sys`)
* User-space utilities (`free`, `vmstat`, `iostat`)
* Systemd journal and logs

**Key principle:** You do not troubleshoot blindly — you observe, confirm, then act.

---

## Kernel and OS Identity

### `uname -a`

Provides kernel version, architecture, and build metadata.

Used to:

* Confirm kernel compatibility
* Debug driver or module issues
* Validate cloud image versions

---

### `hostnamectl`

Manages and displays system hostname and OS metadata.

Production relevance:

* Host identification in clusters
* Log correlation
* CMDB and monitoring alignment

---

## Uptime and Load

### `uptime`

Shows:

* System running time
* Number of users
* Load averages (1, 5, 15 min)

**Important:** Load is not CPU usage — it is runnable + blocked processes.

---

## Memory Visibility

### `free -h`

Displays:

* Total memory
* Used / free
* Buffers and cache
* Swap usage

Linux aggressively uses memory for cache. Free memory alone is not a problem.

---

### `vmstat`

Provides insight into:

* Memory pressure
* Context switching
* CPU wait states

Used for identifying system stress patterns.

---

## CPU and I/O Metrics

### `iostat`

Used to identify:

* Disk latency
* I/O bottlenecks
* Saturated devices

---

### `mpstat`

Shows per-CPU usage.

Critical in:

* Multi-core imbalance detection
* Pinpointing CPU saturation

---

### `pidstat`

Per-process CPU, memory, and I/O statistics.

Used when:

* A specific service is misbehaving
* Identifying noisy neighbors

---

## Hardware Inventory

### `lscpu`

CPU architecture, cores, threads, NUMA layout.

---

### `lsusb` / `lspci`

Enumerates connected USB and PCI devices.

Useful for:

* VM vs bare-metal validation
* Driver troubleshooting

---

### `lshw`

Detailed hardware inventory.

Often used during:

* Capacity planning
* Incident RCA documentation

---

## Kernel and System Logs

### `dmesg`

Displays kernel ring buffer messages.

Used for:

* Boot diagnostics
* Hardware and driver issues

---

### `journalctl`

Systemd’s centralized logging system.

Key usages:

* `journalctl -xe` — recent critical events
* `journalctl -u nginx` — service-specific logs

**Production rule:** Logs are evidence. Never guess when logs exist.

---

## Why This Matters in DevOps

You will use these tools to:

* Diagnose outages
* Validate deployments
* Investigate performance issues
* Support production incidents
* Provide accurate RCAs

If you cannot read system state and logs, you cannot operate production systems.

---

## Next Step

Proceed to the [**System Information & Logs – Hands-On Lab**](../../../98-home-lab/labs/01-linux/08-system-information-and-logs/README.md) to build operational confidence.
