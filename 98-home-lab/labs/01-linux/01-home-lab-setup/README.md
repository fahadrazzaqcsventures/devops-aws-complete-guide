# Home Lab Setup – Linux-First DevOps Foundation

## Objective

Build a **Linux-first DevOps home lab** that is:

* Reproducible
* Well-documented
* Destroyable
* Suitable for gradual progression into DevOps and AWS

This home lab focuses on **fundamentals before tools**, using local hardware first and cloud resources only when they add real engineering value.

---

## Lab Scope (Current Phase)

**Phase:** Linux Fundamentals

**What this lab is for:**

* Learning Linux system administration
* Practicing real server management tasks
* Building habits used in production environments

**What this lab is NOT for (yet):**

* Kubernetes
* CI/CD pipelines
* Terraform
* Heavy AWS usage

---

## Hardware Used

| Component                         | Purpose                                 |
| --------------------------------- | --------------------------------------- |
| Personal Laptop                   | Control node, SSH client, documentation |
| Old Laptop (8 GB RAM, 500 GB HDD) | Primary Linux lab server                |
| Raspberry Pi 3 B+                 | Future monitoring / edge node           |
| AWS Account                       | Future production simulation            |

---

## Architecture (Current State)

* One Ubuntu Server acting as the lab server
* Accessed remotely via SSH
* Static IP on local network
* Managed entirely from terminal

---

## Objective of This Setup

* Install a clean Ubuntu Server
* Secure remote access
* Create a non-root admin user
* Establish a baseline that can be rebuilt or destroyed safely

This baseline will be reused for **all future DevOps labs**.

---

## Steps

### Step 1: Install Ubuntu Server

* Install **Ubuntu Server 22.04 LTS** on the old laptop
* Minimal installation
* Enable OpenSSH during setup

---

### Step 2: Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

### Step 3: Create Non-Root User

```bash
sudo adduser devops
sudo usermod -aG sudo devops
```

---

### Step 4: Configure SSH Key-Based Authentication

On personal laptop:

```bash
ssh-keygen -t ed25519
ssh-copy-id devops@<lab-server-ip>
```

---

### Step 5: Secure SSH

Edit SSH configuration:

```bash
sudo nano /etc/ssh/sshd_config
```

Ensure:

```text
PermitRootLogin no
PasswordAuthentication no
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

---

### Step 6: Set Static IP (Recommended)

Configure Netplan so the server IP does not change.

This is critical for:

* Monitoring
* Automation
* Future CI/CD integrations

---

## Validation

Verify each requirement explicitly.

### SSH Access

```bash
ssh devops@<lab-server-ip>
```

Expected result:

* Login succeeds without password
* Root login is denied

---

### User Privileges

```bash
whoami
sudo -l
```

Expected result:

* Logged in as `devops`
* Sudo access works

---

### Service Status

```bash
systemctl status ssh
```

Expected result:

* SSH service is active and enabled

---

## Rollback (Destroyability)

Rollback steps must always exist.

### Remove User

```bash
sudo userdel -r devops
```

---

### Revert SSH Settings

Edit:

```bash
sudo nano /etc/ssh/sshd_config
```

Revert to:

```text
PermitRootLogin yes
PasswordAuthentication yes
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

---

### Full Reset (If Required)

* Reinstall Ubuntu Server
* Reapply this README from scratch

If the system can be rebuilt using this document alone, the lab is **reproducible**.

---

## Why This Matters

This setup demonstrates:

* Linux administration fundamentals
* Security-first mindset
* Documentation discipline
* Production-style thinking

This is the foundation upon which:

* Docker
* CI/CD
* Kubernetes
* Terraform
* AWS

will later be layered.

---

**Status:** Linux Home Lab Baseline Established
