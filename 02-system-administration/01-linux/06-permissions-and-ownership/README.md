# Permissions & Ownership (Theory)

## Purpose

This document explains **how Linux controls access to files and directories** using permissions, ownership, and Access Control Lists (ACLs). For DevOps, SRE, and Cloud engineers, this knowledge is critical because **misconfigured permissions are a leading cause of outages, security incidents, and broken deployments**.

This is theory-first: *how Linux enforces access control and why it behaves the way it does*.

---

## Linux Permission Model

Every file and directory in Linux has:

1. **An owner (user)**
2. **A group**
3. **Permission bits** for:

   * Owner
   * Group
   * Others

Permissions define **who can read, write, or execute** an object.

---

## Permission Types

| Permission | Symbol | Meaning (File) | Meaning (Directory) |
| ---------- | ------ | -------------- | ------------------- |
| Read       | r      | View contents  | List directory      |
| Write      | w      | Modify file    | Create/delete files |
| Execute    | x      | Run file       | Enter directory     |

> Directory execute (`x`) controls **access**, not execution.

---

## Permission Representation

Example:

```
-rwxr-xr--
```

Breakdown:

* `-` → file type
* `rwx` → owner permissions
* `r-x` → group permissions
* `r--` → others permissions

Numeric (octal) form:

| Permission | Value |
| ---------- | ----- |
| r          | 4     |
| w          | 2     |
| x          | 1     |

Example:

* `644` → `rw-r--r--`
* `755` → `rwxr-xr-x`

---

## Ownership

Each file has:

* **Owner (user)** – creator or assigned user
* **Group** – used for shared access

Commands:

* `chown user:group file`
* `chgrp group file`

Ownership controls **who the permission bits apply to**.

---

## chmod – Changing Permissions

Common patterns:

* `chmod 644 file` → owner can read/write, others read
* `chmod 755 file` → executable, typical for scripts/binaries
* `chmod +x script.sh` → make script executable

> In production, permissions should be **minimal and intentional**.

---

## Default Permissions and umask

`umask` defines which permissions are **removed by default** when new files are created.

Example:

```bash
umask 022
```

Effect:

* Files default to `644`
* Directories default to `755`

This is standard for multi-user Linux systems.

---

## Access Control Lists (ACLs)

ACLs provide **fine-grained permissions** beyond the basic owner/group/other model.

Commands:

* `getfacl file` → view ACLs
* `setfacl -m u:user:rwx file` → grant user explicit access

Use cases:

* Multiple teams accessing the same files
* Temporary access without changing ownership

> ACLs are powerful but should be documented and audited.

---

## Why This Matters in DevOps

Permissions and ownership directly affect:

* Application startup failures
* CI/CD pipeline errors
* Container volume access
* Security posture and compliance

> Most "it works on my machine" issues are permission problems.

---

## Next Step

Proceed to the [**Permissions & Ownership – Practical Lab**](../../../98-home-lab/labs/01-linux/06-permissions-and-ownership/README.md) to build hands-on confidence.
