# Firewall Management – Hands-On Lab

## Objective

Build **safe, production-aligned firewall skills** by inspecting rules and applying controlled changes without causing outages.

By the end of this lab, you will:

* Inspect firewall state
* Enable and manage basic rules
* Understand how different firewall tools interact

---

## Lab Environment

* OS: Ubuntu Server 22.04
* User: Non-root user with `sudo`
* Access: SSH enabled

⚠️ Ensure you have console or VM access before modifying firewall rules.

---

## Step 1: Verify SSH Connectivity

Before touching the firewall:

```bash
whoami
ss -tuln | grep :22
```

Confirm:

* SSH service is running
* Port 22 is listening

---

## Step 2: Inspect Existing Firewall Rules

```bash
sudo iptables -L
```

Understand:

* Default policies
* Existing chains

---

## Step 3: Inspect UFW Status

```bash
sudo ufw status verbose
```

If inactive, note current state.

---

## Step 4: Enable UFW Safely

```bash
sudo ufw allow 22
sudo ufw enable
```

Critical rule:

* SSH must be allowed **before** enabling

---

## Step 5: Validate Firewall Rules

```bash
sudo ufw status
sudo iptables -L
```

Confirm:

* SSH access remains available
* Rules are applied

---

## Step 6: firewalld Inspection (If Installed)

```bash
sudo firewall-cmd --list-all
```

Observe:

* Active zone
* Allowed services and ports

---

## Step 7: Test Connectivity

From another terminal or host:

```bash
ssh user@host
```

Ensure connectivity is not broken.

---

## Step 8: Disable Firewall (Rollback Practice)

```bash
sudo ufw disable
```

Understand rollback importance.

---

## Validation Checklist

You can confidently:

* Inspect firewall rules without panic
* Enable firewall safely
* Ensure SSH access remains intact
* Identify which firewall tool is active

---

## Common Production Mistakes

* Enabling firewall without allowing SSH
* Mixing tools blindly (ufw + iptables)
* Making changes without rollback access

---

## Cleanup

Ensure system state:

```bash
sudo ufw disable
```

---

## Outcome

You now have **baseline Linux firewall management skills**.

This directly enables:

* Secure server hardening
* Cloud security group understanding
* Kubernetes node security
* Safe production operations
