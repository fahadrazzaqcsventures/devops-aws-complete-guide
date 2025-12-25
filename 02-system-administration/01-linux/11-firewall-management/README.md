# Linux Fundamentals: Firewall Management (Theory)

## Purpose

This document explains **how Linux firewalls work, how traffic is filtered, and how to manage firewall rules safely in production environments**.

Firewall misconfiguration is one of the **top causes of self-inflicted outages**. For DevOps and SRE engineers, firewall management must be:

* Intentional
* Auditable
* Reversible

This is theory-first: *how packet filtering actually works inside Linux* and *why different firewall tools exist*.

---

## Linux Firewall Mental Model

Linux firewalling happens inside the **kernel networking stack**.

```
Incoming Packet
   ↓
Netfilter Hooks
   ↓
Firewall Rules (Allow / Drop / Reject)
   ↓
Application Socket
```

All firewall tools ultimately manipulate **netfilter**.

---

## Firewall Layers in Linux

Linux commonly exposes three management layers:

1. **iptables** – low-level, rule-based
2. **firewalld** – dynamic, zone-based abstraction
3. **ufw** – simplified frontend (Ubuntu-focused)

Different tools — same kernel engine.

---

## iptables (Low-Level Control)

`iptables` directly manages kernel firewall rules.

Characteristics:

* Powerful
* Verbose
* Easy to break connectivity

Inspect rules:

```bash
iptables -L
```

Production relevance:

* Kubernetes nodes
* Custom networking
* Legacy systems

---

## firewalld (Enterprise Standard)

`firewalld` provides **zone-based** firewall management.

Key ideas:

* Zones (public, internal, trusted)
* Runtime vs permanent rules

Inspect configuration:

```bash
firewall-cmd --list-all
```

Common in:

* RHEL / CentOS / Rocky Linux
* Enterprise environments

---

## UFW (Uncomplicated Firewall)

UFW is a **human-friendly firewall interface**.

Designed for:

* Ubuntu servers
* Simplicity over flexibility

Common commands:

```bash
ufw enable
ufw allow 22
```

UFW internally generates iptables rules.

---

## Allow vs Deny Philosophy

Firewall rules answer one question:

> Should this packet be allowed or blocked?

Best practice:

* Default deny (block everything)
* Explicit allow (open only what is needed)

---

## Ports, Protocols, and State

Firewall rules are based on:

* Protocol (TCP, UDP, ICMP)
* Port numbers
* Connection state (NEW, ESTABLISHED)

Stateful firewalls reduce rule complexity and risk.

---

## Firewalls and Services

Services must:

* Be listening on the correct port
* Be allowed by firewall rules

Firewall debugging always requires:

* Checking service status
* Checking listening ports
* Checking firewall rules

---

## Production Safety Rules

Never:

* Apply firewall changes blindly over SSH
* Lock yourself out without recovery access

Always:

* Verify SSH access is allowed
* Test rules incrementally
* Keep rollback paths

---

## Why This Matters in DevOps

Firewall management is critical when:

* Hardening servers
* Deploying cloud instances
* Exposing applications
* Securing CI/CD agents
* Operating Kubernetes nodes

A single bad rule can cause a full outage.

---

## Next Step

Proceed to [**Firewall Management – Hands-On Lab**](../../../98-home-lab/labs/01-linux/11-firewall-management/README.md) to practice safe inspection and controlled rule changes.
