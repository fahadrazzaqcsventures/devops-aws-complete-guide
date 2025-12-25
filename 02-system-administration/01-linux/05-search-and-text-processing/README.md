# Search & Text Processing (Theory)

## Purpose

This document explains **how Linux engineers search, filter, and process text efficiently**. Mastery of search and text processing is critical for DevOps, SREs, and Cloud engineers because **logs, configuration files, and command outputs need to be parsed, transformed, and analyzed routinely**.

This is theory-first: *why* commands exist and *how* they behave in production.

---

## Text Processing Philosophy

Linux provides tools for **searching, transforming, and formatting text**. These tools can be combined in pipelines for powerful automation.

> **Design principle:** Build small commands that do one thing well and chain them for complex tasks.

---

## Core Commands

| Command                     | Purpose                            | Notes / Production Relevance                             |
| --------------------------- | ---------------------------------- | -------------------------------------------------------- |
| `grep "pattern" file`       | Search pattern in a file           | Quick search in configs or logs                          |
| `grep -ri "pattern" dir/`   | Recursive, case-insensitive search | Search across directories, logs, and source code         |
| `sort file`                 | Sort lines alphabetically          | Useful for ordering logs or config entries               |
| `uniq file`                 | Remove repeated adjacent lines     | Common after `sort` to find unique entries               |
| `cut -d ':' -f 1 file`      | Select delimited fields            | Extract usernames, IPs, or other structured data         |
| `awk '{print $1}' file`     | Print the first column             | Powerful for structured text parsing                     |
| `sed -i 's/old/new/g' file` | In-place find and replace          | Modify configs or templates programmatically             |
| `tr 'a-z' 'A-Z'`            | Translate characters               | Convert text between cases or character sets             |
| `paste file1 file2`         | Merge lines side by side           | Combine related data from multiple files                 |
| `tee out.txt`               | Write output to file and stdout    | Useful for logging intermediate results while processing |

---

## Choosing the Right Tool

* **Search for text** → `grep`
* **Sorting and deduplication** → `sort` + `uniq`
* **Field extraction** → `cut`, `awk`
* **In-place editing** → `sed`
* **Character translation** → `tr`
* **Merging files** → `paste`
* **Output capture** → `tee`

---

## Why This Matters in DevOps

You will use these commands when:

* Debugging applications and containers
* Parsing and analyzing logs
* Automating configuration updates
* Processing command outputs
* Generating reports from multiple sources

> Mastery allows fast troubleshooting, accurate automation, and efficient text handling in production environments.

---

## Next Step

Proceed to the [**Linux Search & Text Processing – Practical Lab**](../../../98-home-lab/labs/01-linux/05-search-and-text-processing/README.md) for hands-on exercises.
