# Disks, Partitions, and Filesystems – Hands-On Lab

## Objective

Develop **operational confidence** inspecting disks, understanding partitions, checking filesystem usage, and performing safe mount operations.

This lab avoids destructive actions unless explicitly stated.

---

## Lab Environment

* OS: Ubuntu Server 22.04
* User: Non-root user with `sudo`
* Environment: VM or lab server

---

## Step 1: Inspect Filesystem Usage

```bash
df -h
```

Understand:

* Mounted filesystems
* Disk usage percentage

---

## Step 2: Identify Large Directories

```bash
du -sh /var/*
```

Use case:

* Finding disk usage hotspots

---

## Step 3: Inspect Block Devices

```bash
lsblk
blkid
```

Validate:

* Disk vs partition layout
* Filesystem types

---

## Step 4: Inspect Partition Tables

```bash
sudo fdisk -l
sudo parted -l
```

Observe:

* Disk sizes
* Partition boundaries

Do **not** modify anything.

---

## Step 5: (Optional / VM Only) Create a Filesystem

⚠️ Perform this step **only on a disposable VM disk**.

```bash
sudo mkfs.ext4 /dev/sdX1
```

Understand:

* Filesystem creation is destructive

---

## Step 6: Mount and Unmount a Filesystem

```bash
sudo mkdir -p /mnt/testdisk
sudo mount /dev/sdX1 /mnt/testdisk
mount | grep testdisk
```

Then unmount:

```bash
sudo umount /mnt/testdisk
```

---

## Step 7: View Persistent Mount Configuration

```bash
cat /etc/fstab
```

Understand:

* UUID-based mounts
* Boot-time implications

---

## Step 8: Filesystem Health Check (Read-Only)

```bash
sudo fsck -n /dev/sdX1
```

`-n` prevents modifications.

---

## Validation Checklist

You can confidently:

* Differentiate disk, partition, and filesystem
* Identify disk usage issues
* Mount and unmount filesystems safely
* Explain `/etc/fstab` risks

---

## Common Production Mistakes

* Formatting the wrong device
* Running `fsck` on mounted filesystems
* Editing `/etc/fstab` without recovery access

---

## Rollback / Cleanup

```bash
sudo umount /mnt/testdisk
sudo rmdir /mnt/testdisk
```

---

## Outcome

You now have **production-grade understanding of Linux storage fundamentals**, a prerequisite for cloud volumes, Kubernetes storage, and incident response.
