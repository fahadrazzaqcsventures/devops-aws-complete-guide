# Package Management (Theory)

## Purpose

This document explains **how software is installed, upgraded, verified, and removed on Linux systems** using package managers. Package management is a critical operational skill for DevOps and SRE roles because:

* Every server, container, and CI agent depends on managed packages
* Security patching relies on correct upgrade workflows
* Broken packages are a common root cause of outages

This is theory-first: *how package systems work internally and why best practices exist*.

---

## What Is a Package Manager

A **package manager** automates the lifecycle of software:

* Downloading binaries
* Resolving dependencies
* Verifying integrity
* Installing files into correct locations
* Tracking versions for upgrades and removal

On Debian/Ubuntu systems, the ecosystem consists of:

* **APT** (high-level package manager)
* **dpkg** (low-level package tool)

---

## APT vs DPKG

| Tool        | Role                          | Production Usage            |
| ----------- | ----------------------------- | --------------------------- |
| `apt-get`   | High-level package management | Daily operations            |
| `apt-cache` | Package metadata queries      | Discovery & debugging       |
| `dpkg`      | Low-level package installer   | Emergency / manual installs |

**Rule:** Use `apt`/`apt-get` whenever possible. Use `dpkg` only when required.

---

## Package Repositories

APT pulls software from **repositories** defined in:

* `/etc/apt/sources.list`
* `/etc/apt/sources.list.d/`

Repositories provide:

* Versioned packages
* Security updates
* Signed metadata

> Trust is established through **GPG signing** of repositories.

---

## Package Metadata and Dependency Resolution

Each package defines:

* Required dependencies
* Optional recommendations
* Conflicting packages

APT automatically resolves these relationships, preventing:

* Missing libraries
* Incompatible versions
* Partial installations

This is why manual binary installs are discouraged in production.

---

## Package Lifecycle Operations

### Refreshing Package Lists

```bash
apt-get update
```

* Downloads repository metadata
* Does **not** install or upgrade anything

Must be run before installs or upgrades.

---

### Installing Packages

```bash
apt-get install nginx
```

* Resolves dependencies
* Downloads packages
* Installs files under standard paths

---

### Upgrading Packages

```bash
apt-get upgrade
```

* Upgrades installed packages
* Does not remove packages or install new dependencies

Used for **safe routine patching**.

---

### Removing Packages

```bash
apt-get remove pkg
```

* Removes binaries
* Leaves configuration files

Used when rollback or reinstallation may be required.

---

## Package Discovery and Inspection

### Searching Packages

```bash
apt-cache search nginx
```

### Viewing Package Details

```bash
apt-cache show pkg
```

Used to:

* Validate package source
* Check version and dependencies
* Review package description

---

## DPKG and Local Packages

### Installing a Local .deb

```bash
dpkg -i pkg.deb
```

* Installs a package file directly
* Does **not** resolve dependencies automatically

### Removing a Package

```bash
dpkg -r pkg
```

Used mainly for:

* Vendor-provided packages
* Debugging broken installs

---

## Why This Matters in DevOps

You will manage packages when:

* Building base images
* Patching CVEs
* Managing CI/CD runners
* Installing agents (monitoring, security, logging)
* Debugging broken nodes

Poor package hygiene leads to **unstable, insecure systems**.

---

## Next Step

Proceed to the [**Package Management – Hands-On Lab**](../../../98-home-lab/labs/01-linux/13-package-management/README.md) to practice safe installation, upgrades, and inspection workflows.
