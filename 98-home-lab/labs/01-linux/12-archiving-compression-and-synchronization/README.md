# Archiving, Compression, and Synchronization (Lab)

## Lab Objectives

By completing this lab, you will:

* Create and extract archives
* Apply different compression algorithms
* Synchronize data locally and remotely
* Understand real-world DevOps use cases

All exercises are safe to run on a local VM or home lab.

---

## Lab Setup

Create a working directory:

```bash
mkdir -p ~/archive-lab/data
cd ~/archive-lab
echo "file one" > data/file1.txt
echo "file two" > data/file2.txt
```

---

## Exercise 1: tar Archives

Create a tar archive:

```bash
tar -cf archive.tar data/
```

Extract it:

```bash
mkdir extracted
tar -xf archive.tar -C extracted/
```

Verify contents:

```bash
ls extracted/data
```

---

## Exercise 2: tar with gzip

Create compressed archive:

```bash
tar -czf archive.tar.gz data/
```

Extract:

```bash
tar -xzf archive.tar.gz
```

---

## Exercise 3: zip Archives

Create zip file:

```bash
zip -r archive.zip data/
```

Extract:

```bash
unzip archive.zip
```

---

## Exercise 4: Standalone Compression

gzip:

```bash
gzip data/file1.txt
ls data/
gunzip data/file1.txt.gz
```

bzip2:

```bash
bzip2 data/file2.txt
bunzip2 data/file2.txt.bz2
```

xz:

```bash
xz data/file1.txt
unxz data/file1.txt.xz
```

---

## Exercise 5: Local rsync

Create destination:

```bash
mkdir ~/archive-lab/backup
```

Sync files:

```bash
rsync -avz data/ backup/
```

Modify a file and re-run rsync to observe delta transfer.

---

## Exercise 6: rsync Over SSH (Optional)

If you have a second VM or server:

```bash
rsync -avz -e ssh data/ user@host:/tmp/archive-lab/
```

---

## Exercise 7: cpio Archive

Create file list:

```bash
ls data > filelist
```

Create archive:

```bash
cpio -ov < filelist > archive.cpio
```

---

## Validation Checklist

Confirm you can:

* Create and extract tar archives
* Compare compression formats
* Sync data efficiently with rsync
* Understand when not to use full copies

---

## Cleanup

```bash
rm -rf ~/archive-lab
```

---

## DevOps Takeaway

These tools appear everywhere:

* Backup automation
* CI/CD artifact handling
* Data migration
* Incident recovery

Mastery here directly improves reliability and speed.
