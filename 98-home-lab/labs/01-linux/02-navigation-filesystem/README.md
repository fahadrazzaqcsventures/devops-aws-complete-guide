# Linux Navigation & Filesystem – Hands-On Lab

## Objective

Build **muscle memory and operational confidence** navigating a Linux system exactly as required in production environments.

By the end of this lab, you will:

* Navigate the filesystem without guessing
* Identify critical directories
* Inspect files safely
* Understand where applications, logs, and configs live

---

## Lab Environment

* OS: Ubuntu Server 22.04 (VM or bare metal)
* User: Non-root user with `sudo` access
* No GUI

---

## Step 1: Identify Your Location

```bash
pwd
```

Expected:

* Output starts with `/`
* You understand where you are before acting

---

## Step 2: Explore Root Structure

```bash
cd /
ls
```

Validate:

* You can identify `/etc`, `/var`, `/home`, `/usr`
* Nothing here is random

---

## Step 3: Inspect Configuration Directory

```bash
cd /etc
ls
```

Observe:

* Service-specific folders
* Plain-text configuration files

Do **not** edit anything yet.

---

## Step 4: Navigate Logs Safely

```bash
cd /var/log
ls
```

View logs without modifying them:

```bash
ls -lh
```

Understand:

* Logs grow continuously
* Disk space issues often originate here

---

## Step 5: Move Between Directories Efficiently

```bash
cd /
cd ~
pwd
cd ..
pwd
cd -
```

Learn:

* `/` is your root directory
* `~` is your home directory
* `..` is parent
* `cd -` toggles previous location

---

## Step 6: Absolute vs Relative Paths

```bash
cd /etc
ls vim
ls /etc/vim
```

Confirm:

* Both commands work
* Absolute paths are safer in scripts

---

## Step 7: Hidden Files

```bash
cd ~
ls
ls -a
```

Identify:

* `.bashrc`
* `.profile`

These control shell behavior.

---

## Validation Checklist

You can confidently:

* Explain what `/etc`, `/var`, `/home` contain
* Move anywhere without trial-and-error
* Use `ls` flags intentionally
* Avoid destructive commands

---

## Common Production Mistakes

* Editing files directly in `/etc` without backups
* Running commands without knowing current directory
* Using relative paths in automation

Avoid these habits early.

---

## Rollback / Cleanup

This lab is **read-only**.

No system state was modified.
Nothing to rollback.

---

## Outcome

You now possess **baseline Linux operational literacy**.

This is the foundation for:

* Shell scripting
* Docker
* Kubernetes
* CI/CD agents
* Cloud instances

Next lab builds on this skill — not replaces it.
