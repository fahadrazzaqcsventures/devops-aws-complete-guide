# Linux File & Directory Management – Hands-On Lab

## Objective

Build **muscle memory and operational confidence** managing files and directories in Linux. By the end of this lab, you will:

* Navigate the filesystem without guessing
* Create, copy, move, and delete files and directories safely
* Inspect file metadata and timestamps
* Understand where critical files, logs, and configs live

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
* Understand your current working directory

---

## Step 2: Explore Root Structure

```bash
cd /
ls
```

Validate:

* Identify `/etc`, `/var`, `/home`, `/usr`
* Nothing is random

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
ls -lh
```

Understand:

* Logs grow continuously
* Disk space issues often originate here

---

## Step 5: Create Files and Directories

```bash
cd ~
touch file.txt        # create empty file
mkdir dir              # create directory
mkdir -p a/b/c         # nested directories
```

---

## Step 6: Copy and Move

```bash
cp file.txt copy.txt       # copy file
cp -r dir dir_copy          # copy directory recursively
mv file.txt file_renamed    # rename or move
```

---

## Step 7: Remove Files and Directories

```bash
rm file_renamed         # remove file
rm -rf dir_copy          # remove directory tree (use caution)
rmdir a/b/c              # remove empty directory
```

---

## Step 8: Explore Hidden Files

```bash
cd ~
ls
ls -a
```

Identify:

* `.bashrc`
* `.profile`

---

## Step 9: Inspect File Metadata

```bash
stat file.txt
```

Observe:

* Access, modification, and change timestamps
* Permissions and ownership

---

## Step 10: Absolute vs Relative Paths

```bash
cd /etc
ls vim
ls /etc/vim
```

Confirm:

* Both commands work
* Absolute paths are safer in scripts

---

## Validation Checklist

You can confidently:

* Explain contents of `/etc`, `/var`, `/home`
* Move anywhere without trial-and-error
* Use `ls`, `cp`, `mv`, `rm`, `mkdir`, and `stat` correctly
* Understand hidden files and their purpose

---

## Common Production Mistakes

* Editing files directly in `/etc` without backups
* Running commands without knowing current directory
* Using relative paths in automation

---

## Rollback / Cleanup

This lab is **read-only**. Minimal changes were made and can be safely removed.

---

## Outcome

You now possess **baseline Linux operational literacy**, foundational for:

* Shell scripting
* Docker and Kubernetes
* CI/CD agents
* Cloud instances

Next labs will build on these skills.
