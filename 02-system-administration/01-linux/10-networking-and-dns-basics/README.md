# Linux Fundamentals: Networking and DNS (Theory)

## Purpose

This document explains **how Linux networking works, how systems communicate, and how DNS resolves names to IP addresses**.

For DevOps, SRE, and Cloud engineers, networking is **non-optional**:

* If networking is broken, everything is broken
* Most production outages are network or DNS related

This is theory-first: *how Linux sees the network* and *how to reason about failures systematically*.

---

## Linux Networking Mental Model

At a high level:

```
Application
   ↓
Socket (IP:Port)
   ↓
Routing Table
   ↓
Network Interface
   ↓
Physical / Virtual Network
```

Linux does not "send packets magically". Every packet follows this path.

---

## Network Interfaces and IP Addresses

Linux manages interfaces and IPs via the kernel networking stack.

Inspect IP configuration:

```bash
ip addr
```

Key concepts:

* Interfaces (eth0, ens33, lo)
* IPv4 vs IPv6
* Subnet masks and CIDR

Loopback (`lo`) is critical for local services.

---

## Routing and Gateways

Routing decides **where packets go**.

View routing table:

```bash
ip route
```

Important entries:

* Default gateway
* Directly connected networks

Misconfigured routes cause silent failures.

---

## Connectivity Testing

### ICMP

```bash
ping -c 4 host
```

Used to:

* Test reachability
* Measure latency

Ping working does **not** guarantee application connectivity.

---

### Path Analysis

```bash
traceroute host
```

Shows hop-by-hop packet path.

Used for:

* Identifying network bottlenecks
* Diagnosing routing issues

---

## Ports, Sockets, and Services

Services listen on **IP + Port** combinations.

Inspect listening services:

```bash
ss -tuln
netstat -tuln
```

Production relevance:

* Verify services are listening
* Detect port conflicts

---

## DNS Fundamentals

DNS resolves **names → IP addresses**.

Without DNS, modern infrastructure fails.

Query DNS:

```bash
nslookup example.com
dig example.com
```

`dig` provides:

* Record types
* TTLs
* Authority

DNS failures are often mistaken for application bugs.

---

## HTTP and File Transfer

### HTTP Requests

```bash
curl -I https://example.com
```

Used to:

* Validate HTTP headers
* Test TLS and connectivity

---

### File Downloads

```bash
wget https://example.com/file
```

Used in automation, CI/CD, and bootstrap scripts.

---

## Secure Remote Access

### SSH

```bash
ssh user@host
```

Foundation of:

* Server administration
* Automation
* CI/CD agents

---

### File Transfer over SSH

```bash
scp file user@host:/path/
sftp user@host
```

Used for:

* Secure file movement
* Emergency recovery

---

## Low-Level Networking Tools

### Netcat

```bash
nc -l -p 1234
nc host 80
```

Used for:

* Port testing
* Debugging services

---

### Packet Capture

```bash
tcpdump -i eth0 port 443
```

Used when:

* Traffic exists but applications fail
* Debugging TLS or protocol issues

---

### Port Scanning

```bash
nmap -sS host
```

Used for:

* Security validation
* Exposure analysis

---

## Firewalls

Linux filtering happens via kernel firewall rules.

### UFW (Simple)

```bash
ufw enable
ufw allow 22
```

---

### iptables (Low-level)

```bash
iptables -L
```

---

### firewalld (Enterprise)

```bash
firewall-cmd --list-all
```

Firewall misconfiguration is a top cause of outages.

---

## Why This Matters in DevOps

You will use these skills to:

* Debug service connectivity
* Troubleshoot Kubernetes networking
* Secure cloud instances
* Diagnose CI/CD failures
* Perform incident response

Without networking fundamentals, higher-level tools are useless.

---

## Next Step

Proceed to [**Networking and DNS – Hands-On Lab**](../../../98-home-lab/labs/01-linux/10-networking-and-dns-basics/README.md) to practice safe, production-style diagnostics.
