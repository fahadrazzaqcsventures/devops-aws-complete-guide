# Linux Search & Text Processing – Hands-On Lab

## Objective

Build **practical skills in searching and processing text** on Linux systems. By the end of this lab, you will:

* Search patterns in files and directories
* Sort and deduplicate text
* Extract fields and columns
* Modify files in-place
* Transform and merge text outputs
* Capture outputs for further processing

---

## Lab Environment

* OS: Ubuntu Server 22.04 (VM or bare metal)
* User: Non-root user with `sudo` access
* No GUI

---

## Step 1: Search for Patterns

```bash
grep "pattern" file.txt
grep -ri "pattern" dir/
```

Observe:

* Matches in single files or recursively
* Case-insensitive search with `-i`

---

## Step 2: Sort and Remove Duplicates

```bash
sort file.txt
sort file.txt | uniq
```

Use case:

* Organize log entries or config lines
* Identify unique records

---

## Step 3: Extract Fields

```bash
cut -d ':' -f 1 /etc/passwd
awk '{print $1}' file.txt
```

Observe:

* Extract usernames, IPs, or first column of structured data
* `cut` for delimited files, `awk` for column-based processing

---

## Step 4: In-Place Editing

```bash
sed -i 's/old/new/g' file.txt
```

Use case:

* Modify configuration files programmatically
* Be cautious: always backup important files

---

## Step 5: Character Translation

```bash
tr 'a-z' 'A-Z' < file.txt
```

Observe:

* Convert lowercase to uppercase
* Useful for normalizing text data

---

## Step 6: Merge Files

```bash
paste file1.txt file2.txt
```

Use case:

* Combine related data side by side
* Helpful in log correlation or data reporting

---

## Step 7: Capture Output

```bash
grep "error" logfile.log | tee errors.txt
```

Observe:

* Output is displayed and written to file simultaneously
* Useful for logging intermediate results in pipelines

---

## Validation Checklist

You can confidently:

* Search files and directories with patterns
* Sort and remove duplicate lines
* Extract columns and fields
* Perform in-place find-and-replace
* Translate characters, merge files, and capture output

---

## Common Production Mistakes

* Editing files without backups
* Using grep without proper flags (case-sensitivity, recursion)
* Overwriting important files accidentally with `sed -i`

---

## Rollback / Cleanup

* Restore any backup files if changed
* All outputs from `tee` can be removed safely

---

## Outcome

You now possess **practical skills to search, transform, and process text** in Linux — essential for logs, configs, and automation pipelines in production.
