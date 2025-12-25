# Services, Scheduling, and systemd – Hands-On Lab

## Objective

Build **real operational control** over Linux services and scheduled jobs.

By the end of this lab, you will:

* Control service lifecycle with systemd
* Verify boot persistence
* Inspect service health correctly
* Schedule recurring and one‑time jobs safely

---

## Lab Environment

* OS: Ubuntu Server 22.04
* User: Non‑root user with `sudo`
* Services: nginx installed
* No GUI

---

## Step 1: Inspect Service Status

```bash
systemctl status nginx
```

Understand:

* Active vs inactive
* Loaded unit file
* Recent log output

This is your **primary diagnostic command**.

---

## Step 2: Start and Stop a Service

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
```

Validate:

```bash
systemctl status nginx
```

Observe state transitions.

---

## Step 3: Restart a Service

```bash
sudo systemctl restart nginx
```

Used after:

* Config changes
* Certificate updates
* Deployment events

---

## Step 4: Enable and Disable at Boot

Enable:

```bash
sudo systemctl enable nginx
```

Disable:

```bash
sudo systemctl disable nginx
```

Understand:

* Enabled ≠ running
* Disabled ≠ stopped

---

## Step 5: Legacy Service Commands

```bash
sudo service nginx start
sudo service nginx status
```

Confirm:

* Commands work
* systemd is still managing the service

Use only for compatibility.

---

## Step 6: View Existing Cron Jobs

```bash
crontab -l
```

If none exist, expect:

* "no crontab for user"

---

## Step 7: Create a Cron Job

Edit cron table:

```bash
crontab -e
```

Add:

```cron
*/5 * * * * echo "cron test" >> ~/cron.log
```

Verify:

```bash
crontab -l
```

---

## Step 8: Remove Cron Jobs

```bash
crontab -r
```

Confirm removal:

```bash
crontab -l
```

---

## Step 9: Schedule One‑Time Job

```bash
at 09:00
```

Then type:

```bash
echo "one time job" >> ~/at.log
```

Exit with:

```bash
Ctrl+D
```

---

## Step 10: Batch Execution

```bash
batch
```

Use for:

* CPU‑heavy tasks
* Off‑peak execution

---

## Step 11: Sleep and Delays

```bash
sleep 5s
echo "done"
```

Common in:

* Startup scripts
* CI/CD pipelines

---

## Validation Checklist

You can confidently:

* Start, stop, and restart services
* Control boot persistence
* Inspect service health
* Schedule recurring jobs
* Schedule one‑time tasks

---

## Common Production Mistakes

* Forgetting to enable services at boot
* Restarting without checking status
* Using cron without logging
* Scheduling heavy jobs during peak hours

---

## Rollback / Cleanup

```bash
sudo systemctl stop nginx
sudo systemctl disable nginx
crontab -r
```

System restored to baseline.

---

## Outcome

You now control **service availability and task scheduling**.

This skill is foundational for:

* CI/CD agents
* Kubernetes nodes
* Monitoring stacks
* Production reliability
