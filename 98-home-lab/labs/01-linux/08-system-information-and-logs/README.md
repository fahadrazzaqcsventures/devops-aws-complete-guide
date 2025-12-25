# System Information & Logs – Hands-On Lab

## Objective

Develop **real-world diagnostic skills** by inspecting system information and logs exactly as required during production incidents.

By the end of this lab, you will:

* Identify system characteristics
* Assess CPU, memory, and I/O health
* Inspect kernel and service logs safely

---

## Lab Environment

* OS: Ubuntu Server 22.04
* User: Non-root user with `sudo`
* No GUI

---

## Step 1: Identify Kernel and Host

```bash
uname -a
hostnamectl
```

Validate:

* Kernel version and architecture
* Hostname correctness

---

## Step 2: Check Uptime and Load

```bash
uptime
```

Understand:

* Load averages trend
* Whether system is under stress

---

## Step 3: Inspect Memory Usage

```bash
free -h
vmstat 1 5
```

Observe:

* Memory vs cache usage
* Swap behavior

---

## Step 4: CPU and I/O Visibility

```bash
iostat
mpstat
pidstat
```

Identify:

* Disk latency
* CPU imbalance
* High-resource processes

---

## Step 5: Hardware Inspection

```bash
lscpu
lsusb
lspci
sudo lshw | less
```

Confirm:

* CPU layout
* Attached devices

---

## Step 6: Kernel Diagnostics

```bash
dmesg | less
```

Look for:

* Errors
* Warnings
* Hardware issues

---

## Step 7: System and Service Logs

```bash
journalctl -xe
journalctl -u nginx
```

Practice:

* Reading logs without modifying state
* Identifying failure patterns

---

## Validation Checklist

You can confidently:

* Identify system health
* Interpret load and memory correctly
* Trace issues using logs
* Support incident investigations

---

## Common Production Mistakes

* Confusing cache usage with memory leaks
* Ignoring load averages
* Skipping logs and guessing

---

## Rollback / Cleanup

This lab is **read-only**.

No system changes were made.

---

## Outcome

You now have **baseline system observability skills**.

This directly enables:

* Troubleshooting CI/CD agents
* Debugging containers and nodes
* Operating cloud instances
* Incident response participation
