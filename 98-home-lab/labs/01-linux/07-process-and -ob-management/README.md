# Processes & Jobs – Hands-On Lab

## Objective

Build **real operational confidence** managing processes and shell jobs as required in production Linux environments.

By the end of this lab, you will:

* Identify and inspect running processes
* Control process execution safely
* Manage foreground and background jobs
* Observe system behavior in real time

---

## Lab Environment

* OS: Ubuntu Server 22.04
* User: Non-root user with `sudo`
* Terminal-only (no GUI)

---

## Step 1: View Running Processes

```bash
ps aux
```

Observe:

* USER, PID, CPU, MEM columns
* Command arguments

---

## Step 2: Real-Time Monitoring

```bash
top
```

Actions:

* Sort by CPU and memory
* Identify the busiest process

Exit with `q`.

If available:

```bash
htop
```

---

## Step 3: Find Processes by Name

```bash
pgrep systemd
```

Confirm:

* Multiple PIDs may exist

---

## Step 4: Start and Terminate a Test Process

```bash
sleep 300 &
pgrep sleep
kill PID
```

Replace `PID` with the actual value.

Understand:

* Background execution
* Graceful termination

---

## Step 5: Kill by Name (Controlled)

```bash
sleep 400 &
sleep 500 &
pkill sleep
```

Verify:

```bash
pgrep sleep
```

---

## Step 6: Adjust Process Priority

```bash
nice -n 10 sleep 200 &
pgrep sleep
```

Change priority:

```bash
renice -n 5 -p PID
```

Observe scheduling differences.

---

## Step 7: Job Control

```bash
sleep 600
```

Suspend with:

```bash
Ctrl+Z
jobs
bg %1
fg %1
```

---

## Step 8: Detach from Terminal

```bash
nohup sleep 700 &
```

Logout safety:

* Process survives SSH disconnect

---

## Step 9: Measure Execution Time

```bash
time sleep 2
```

Understand:

* Real vs user vs sys time

---

## Step 10: Live Monitoring with Watch

```bash
watch -n 1 free
```

Observe:

* Memory usage updates every second

Exit with `Ctrl+C`.

---

## Validation Checklist

You can confidently:

* Identify processes consuming resources
* Terminate processes safely
* Control job execution
* Adjust scheduling priority
* Monitor systems live

---

## Common Production Mistakes

* Killing processes blindly with `-9`
* Ignoring process priority
* Confusing jobs with system processes
* Leaving runaway background tasks

---

## Rollback / Cleanup

Terminate any remaining test processes:

```bash
pkill sleep
```

System returns to normal state.

---

## Outcome

You now understand **how Linux executes work and how to control it under pressure**.

This knowledge is foundational for:

* systemd services
* Containers
* Kubernetes nodes
* CI/CD runners
* Production incident response
