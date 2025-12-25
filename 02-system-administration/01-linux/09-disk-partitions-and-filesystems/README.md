# Linux Fundamentals: Disks, Partitions, and Filesystems (Theory)

## Purpose

This document explains **how Linux stores data on disks**, how that storage is divided into partitions, and how filesystems make data usable.

For DevOps and SRE engineers, disk-related incidents are **high-impact and high-risk**:

* Full disks cause outages
* Corrupted filesystems cause data loss
* Incorrect mounts break applications

This is theory-first: *how Linux thinks about storage* and *why mistakes here are expensive*.

---

## Storage Stack Mental Model

Linux storage is layered:

```
Physical Disk
   ↓
Partition Table
   ↓
Partitions
   ↓
Filesystem
   ↓
Mount Point
   ↓
Applications
```

Each layer has a **single responsibility**. Confusing layers leads to destructive errors.

---

## Disks and Block Devices

Linux represents disks as **block devices**.

Examples:

* `/dev/sda` → first disk
* `/dev/sdb` → second disk
* `/dev/nvme0n1` → NVMe disk

Block devices expose raw storage. They contain **no files** until formatted.

Inspect devices:

```bash
lsblk
blkid
```

Production relevance:

* Identifying correct disks before formatting
* Avoiding data destruction

---

## Partitions

A partition is a **logical slice of a disk**.

Examples:

* `/dev/sda1`
* `/dev/sda2`

Partition tables:

* MBR (legacy)
* GPT (modern, preferred)

Inspect partitions:

```bash
fdisk -l
parted -l
```

---

## Filesystems

A filesystem defines **how data is organized and retrieved**.

Common Linux filesystems:

* `ext4` (default, reliable)
* `xfs` (scalable, common on servers)

Creating a filesystem:

```bash
mkfs.ext4 /dev/sdX1
```

⚠️ This **destroys existing data**.

---

## Mounting

Linux does not use drive letters.

A filesystem becomes usable only when **mounted** into the directory tree.

Example:

```bash
mount /dev/sdX1 /mnt
```

After mounting:

* Files appear under `/mnt`
* Applications interact with files, not disks

Unmounting:

```bash
umount /mnt
```

---

## Persistent Mounts: /etc/fstab

`/etc/fstab` defines filesystems mounted at boot.

View only:

```bash
cat /etc/fstab
```

Incorrect entries can:

* Prevent system boot
* Drop systems into recovery mode

---

## Disk Usage vs Directory Usage

Two different questions:

* **Filesystem usage** → `df -h`
* **Directory usage** → `du -sh`

Both are required during incidents.

---

## Filesystem Health

Filesystems can become inconsistent due to:

* Power loss
* Kernel crashes
* Hardware faults

Check and repair:

```bash
fsck /dev/sdX1
```

⚠️ Run only on **unmounted** filesystems.

---

## Why This Matters in DevOps

You will deal with disks when:

* Debugging "disk full" alerts
* Expanding volumes
* Mounting cloud storage
* Managing Kubernetes persistent volumes
* Recovering failed nodes

Mistakes here cause **irreversible damage**.

---

## Next Step

Proceed to [**Disks, Partitions, and Filesystems – Hands-On Lab**](../../../98-home-lab/labs/01-linux/09-disk-partitions-and-filesystems/README.md) to practice safely in a controlled environment.
