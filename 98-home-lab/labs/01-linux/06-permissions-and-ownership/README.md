# Linux Permissions & Ownership – Hands-On Lab

## Objective

Build **practical confidence** in managing Linux permissions, ownership, and ACLs. By the end of this lab, you will:

* Read and interpret permission bits
* Change permissions safely
* Manage file ownership and groups
* Understand default permissions via umask
* Apply and inspect ACLs

---

## Lab Environment

* OS: Ubuntu Server 22.04 (VM or bare metal)
* User: Non-root user with `sudo` access
* No GUI

---

## Step 1: Inspect Current Permissions

```bash
ls -l
```

Observe:

* File type and permission bits
* Owner and group

---

## Step 2: Modify Permissions with chmod

```bash
touch file.txt
chmod 644 file.txt
ls -l file.txt
```

Then:

```bash
chmod 755 file.txt
ls -l file.txt
```

Understand:

* Difference between read/write and execute

---

## Step 3: Make a Script Executable

```bash
touch script.sh
chmod +x script.sh
ls -l script.sh
```

Why this matters:

* Scripts must be executable to run in CI/CD pipelines

---

## Step 4: Change Ownership

```bash
sudo chown user:group file.txt
```

Then:

```bash
sudo chgrp group script.sh
```

Understand:

* Ownership controls which permissions apply

---

## Step 5: Default Permissions with umask

```bash
umask
umask 022
touch newfile.txt
ls -l newfile.txt
```

Observe:

* Default permissions applied to new files

---

## Step 6: Inspect ACLs

```bash
getfacl file.txt
```

Observe:

* User, group, and ACL entries

---

## Step 7: Apply ACLs

```bash
setfacl -m u:user:rwx file.txt
getfacl file.txt
```

Use case:

* Grant specific user access without changing ownership

---

## Validation Checklist

You can confidently:

* Read permission strings and octal values
* Use `chmod`, `chown`, and `chgrp` correctly
* Explain umask behavior
* Inspect and apply ACLs

---

## Common Production Mistakes

* Granting overly permissive access (e.g., `777`)
* Changing ownership instead of using ACLs
* Forgetting umask defaults in automation

---

## Rollback / Cleanup

```bash
rm -f file.txt script.sh newfile.txt
```

Remove ACLs if needed:

```bash
setfacl -b file.txt
```

---

## Outcome

You now have **operational-level understanding of Linux permissions and ownership**, a critical skill for secure, stable DevOps and cloud environments.
