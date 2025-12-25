# Networking and DNS – Hands-On Lab

## Objective

Build **production-grade networking diagnostic skills** using standard Linux tools.

By the end of this lab, you will:

* Inspect network configuration
* Validate routing and connectivity
* Debug DNS and application access
* Safely inspect ports, traffic, and firewall rules

---

## Lab Environment

* OS: Ubuntu Server 22.04
* User: Non-root user with `sudo`
* Network: LAN or VM network

---

## Step 1: Inspect IP Configuration

```bash
ip addr
```

Validate:

* Interface names
* Assigned IP addresses
* Loopback presence

---

## Step 2: Inspect Routing Table

```bash
ip route
```

Confirm:

* Default gateway exists
* Correct outbound interface

---

## Step 3: Test Connectivity

```bash
ping -c 4 8.8.8.8
ping -c 4 google.com
```

Interpretation:

* IP ping works but DNS fails → DNS issue
* Both fail → network or firewall issue

---

## Step 4: Trace Network Path

```bash
traceroute google.com
```

Observe:

* Hop progression
* Packet drops

---

## Step 5: Inspect Listening Ports

```bash
ss -tuln
netstat -tuln
```

Identify:

* Services bound to ports
* Unexpected listeners

---

## Step 6: DNS Inspection

```bash
nslookup example.com
dig example.com
```

Understand:

* Resolved IPs
* Query success or failure

---

## Step 7: HTTP Connectivity

```bash
curl -I https://example.com
```

Validate:

* HTTP response codes
* TLS handshake

---

## Step 8: File Transfers

```bash
wget https://example.com
ssh user@host
scp /etc/hosts user@host:/tmp/
sftp user@host
```

Practice:

* Secure access
* Remote file transfer

---

## Step 9: Low-Level Network Testing

### Netcat

```bash
nc -l -p 1234
nc localhost 1234
```

Used for:

* Port reachability testing

---

### Packet Capture (Read-Only)

```bash
sudo tcpdump -i eth0 port 443
```

Observe:

* Traffic presence
* Packet flow

---

### Port Scanning (Local Only)

```bash
nmap -sS localhost
```

Never scan external systems without authorization.

---

## Step 10: Firewall Inspection

```bash
sudo ufw enable
sudo ufw allow 22
sudo ufw status
sudo iptables -L
sudo firewall-cmd --list-all
```

Understand:

* Rule ordering
* Default policies

---

## Validation Checklist

You can confidently:

* Diagnose connectivity issues
* Separate DNS vs network failures
* Verify service exposure
* Inspect firewall state

---

## Common Production Mistakes

* Assuming DNS works without testing
* Opening ports blindly
* Forgetting firewall rules exist

---

## Rollback / Cleanup

```bash
sudo ufw disable
```

Stop any `nc` listeners.

---

## Outcome

You now have **core Linux networking and DNS operational skills**.

This directly enables:

* Cloud networking
* Kubernetes services and ingress
* CI/CD agent connectivity
* Secure production operations
