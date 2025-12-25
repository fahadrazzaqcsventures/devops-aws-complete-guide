# Troubleshooting Methodology and Log Analysis – Hands-On Lab

## Objective

Build **incident-ready troubleshooting discipline** using Linux logs and system inspection.

By the end of this lab, you will:

* Follow a structured troubleshooting process
* Inspect logs without damaging evidence
* Isolate root causes safely
* Validate recovery correctly

---

## Lab Environment

* OS: Ubuntu Server 22.04
* User: Non-root user with `sudo`
* Services: nginx installed
* No GUI

---

## Scenario

A web service is reported as **unreachable intermittently**.

Your task is to investigate **without restarting anything initially**.

---

## Step 1: Observe System State

Check uptime and load:

```bash
uptime
```

Check memory:

```bash
free -h
```

Check disk usage:

```bash
df -h
```

Do not act yet.

---

## Step 2: Identify the Service

Check service status:

```bash
systemctl status nginx
```

Observe:

* Active state
* Error messages
* Restart attempts

---

## Step 3: Inspect Service Logs

View recent logs:

```bash
journalctl -u nginx --since "10 minutes ago"
```

Focus on:

* Timestamps
* Errors vs warnings

---

## Step 4: Inspect System Logs

Check critical system messages:

```bash
journalctl -xe
```

Check kernel messages:

```bash
dmesg | tail
```

Look for:

* OOM kills
* Disk errors
* Network issues

---

## Step 5: Correlate Evidence

Answer:

* Did system resources degrade?
* Did nginx crash or fail health checks?
* Did the kernel intervene?

Write a short hypothesis before acting.

---

## Step 6: Apply Minimal Fix (If Needed)

Only after evidence:

```bash
sudo systemctl restart nginx
```

Re-check status:

```bash
systemctl status nginx
```

---

## Step 7: Verify Recovery

Confirm service availability:

```bash
curl -I http://localhost
```

Monitor logs:

```bash
journalctl -u nginx -f
```

---

## Validation Checklist

You can confidently:

* Observe before acting
* Use logs to explain failures
* Restart services intentionally
* Verify recovery

---

## Common Production Mistakes

* Restarting immediately
* Ignoring timestamps
* Focusing on only one log source
* Rebooting without evidence

---

## Rollback / Cleanup

No persistent changes were made.

Logs remain intact.

---

## Outcome

You now possess **incident-grade troubleshooting discipline**.

This skill underpins:

* On-call readiness
* Production support
* Senior DevOps responsibility
