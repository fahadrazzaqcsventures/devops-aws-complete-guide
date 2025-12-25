# Linux Fundamentals: Environment Variables and Shell (Theory)

## Purpose

This document explains **how the Linux shell environment works** and how environment variables influence command execution, applications, automation, and services.

For DevOps, SRE, and Cloud engineers, environment variables are not optional knowledge. They control:

* Application configuration
* CI/CD pipelines
* Secrets injection
* Runtime behavior of services and containers

This is theory-first: *how the shell and environment actually behave*.

---

## What Is a Shell?

A **shell** is a command interpreter that:

* Accepts user input
* Expands variables and aliases
* Locates binaries
* Launches processes

Common shells:

* `bash` (most common)
* `sh`
* `zsh`

In production Linux servers, **bash** is the default.

---

## What Are Environment Variables?

Environment variables are **key–value pairs** passed to processes at runtime.

Characteristics:

* Inherited by child processes
* Exist only for the life of a session (unless persisted)
* Used by applications for configuration

Examples:

* `PATH`
* `HOME`
* `USER`
* `AWS_ACCESS_KEY_ID`

> Environment variables are configuration, not code.

---

## Viewing the Environment

The shell maintains an environment table.

Conceptually:

* Every running process has its own environment
* Child processes inherit from the parent shell

Understanding this inheritance is critical for debugging:

* "Why does it work manually but not in cron?"

---

## Variable Expansion

The shell expands variables **before executing commands**.

Syntax:

* `$VAR`

If a variable is not set:

* Expansion results in an empty string

This behavior explains many silent failures in scripts.

---

## Exporting Variables

Variables can be:

* **Shell-local** – visible only in the current shell
* **Exported** – inherited by child processes

Only exported variables affect:

* Subshells
* Scripts
* Applications

---

## Command Resolution and PATH

When you type a command, the shell:

1. Checks aliases
2. Checks shell built-ins
3. Searches directories listed in `PATH`

`PATH` is an ordered list.

Wrong PATH configuration leads to:

* Running wrong binaries
* Security issues
* CI/CD failures

---

## Command History

The shell maintains a **command history**:

* Stored per user
* Useful for auditing and recovery
* Dangerous for secrets if misused

Production guidance:

* Never type secrets directly into shell commands

---

## Aliases

Aliases are **shortcuts**, not commands.

Characteristics:

* Expanded by the shell
* Not visible to scripts by default
* User convenience only

Aliases should never be relied upon in automation.

---

## Why This Matters in DevOps

Environment and shell behavior directly impact:

* CI/CD pipelines
* Docker containers
* Kubernetes pods
* Systemd services
* Cloud CLI tools

Misunderstanding environment scope causes:

* Broken deployments
* Missing credentials
* Inconsistent behavior

---

## Key Takeaway

> The shell controls **how commands are interpreted**.
> Environment variables control **how software behaves**.

Mastery here eliminates an entire class of production bugs.

---

## Next Step

Proceed to [**Environment Variables and Shell – Hands-On Lab**](../../../98-home-lab/labs/01-linux/15-environment-variables-and-shell/README.md) to apply these concepts safely.
