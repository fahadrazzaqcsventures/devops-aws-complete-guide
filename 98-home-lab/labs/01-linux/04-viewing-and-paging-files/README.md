# Linux Viewing & Paging – Hands-On Lab

## Objective

Build **operational confidence** in viewing and navigating file contents in Linux. By the end of this lab, you will:

* Display small and large files
* Inspect first, last, or specific parts of files
* Follow logs in real-time
* Use paging and search efficiently
* Count lines and number output for reference

---

## Lab Environment

* OS: Ubuntu Server 22.04 (VM or bare metal)
* User: Non-root user with `sudo` access
* No GUI

---

## Step 1: View Entire File

```bash
cat file.txt
```

Observe:

* Entire file content printed
* Fast for small files

---

## Step 2: View File in Reverse

```bash
tac file.txt
```

Use case:

* Inspect most recent entries last-first (useful for logs)

---

## Step 3: Head & Tail

```bash
head -n 20 file.txt       # first 20 lines

tail -n 20 file.txt       # last 20 lines
```

Use case:

* Quickly check beginnings or endings of logs/configs

---

## Step 4: Follow Logs in Real-Time

```bash
tail -f logfile.log
```

Observe:

* New entries appear as they are written
* Press `Ctrl+C` to stop

---

## Step 5: Paging Through Large Files

```bash
less largefile.txt
```

Navigation:

* `Space` → next page
* `b` → previous page
* `/search_term` → search
* `q` → quit

Alternative:

```bash
more largefile.txt
```

* Basic scrolling
* Less interactive than `less`

---

## Step 6: Line Numbering & Counting

```bash
nl file.txt        # show numbered lines
wc -l file.txt     # count lines
```

Use case:

* Reference specific lines in configs or logs
* Determine file size quickly

---

## Validation Checklist

You can confidently:

* View entire files or parts safely
* Scroll and search through large files
* Follow logs in real-time
* Number lines and count entries
* Choose the right command based on file size and use case

---

## Common Production Mistakes

* Using `cat` on very large files (can hang terminal)
* Forgetting `tail -f` for real-time monitoring
* Editing files instead of viewing during troubleshooting

---

## Rollback / Cleanup

No system state is modified.
All viewing and paging is read-only.

---

## Outcome

You now have **practical skills to inspect, monitor, and analyze files** in Linux — a core requirement for DevOps, SRE, and cloud engineers. Next labs will build on this skill by combining file inspection with scripting and automation.
