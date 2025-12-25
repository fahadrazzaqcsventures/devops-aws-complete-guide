# Linux Fundamentals: Package Management – Hands-On Lab

## Objective

Develop **operational confidence** managing software packages on a production-style Ubuntu system.

By the end of this lab, you will:

* Safely refresh repositories
* Install and remove packages
* Inspect package metadata
* Understand when to use APT vs DPKG

---

## Lab Environment

* OS: Ubuntu Server 22.04
* User: Non-root user with `sudo` access
* Internet access required

---

## Step 1: Refresh Package Index

```bash
sudo apt-get update
```

Validate:

* No repository errors
* Metadata downloads successfully

Never skip this step before installs.

---

## Step 2: Search for a Package

```bash
apt-cache search nginx
```

Observe:

* Multiple related packages
* Distinction between server, docs, and modules

---

## Step 3: Inspect Package Details

```bash
apt-cache show nginx
```

Review:

* Version
* Dependencies
* Maintainer

This is critical in regulated or production environments.

---

## Step 4: Install a Package

```bash
sudo apt-get install nginx
```

Confirm:

* Dependencies resolved automatically
* Service installed correctly

Verify installation:

```bash
nginx -v
```

---

## Step 5: Upgrade Installed Packages

```bash
sudo apt-get upgrade
```

Understand:

* Only installed packages are upgraded
* No packages are removed

This is standard patching behavior.

---

## Step 6: Remove a Package

```bash
sudo apt-get remove nginx
```

Note:

* Configuration files remain
* Allows clean reinstallation

---

## Step 7: Install a Local .deb Package (Optional)

Download a sample package:

```bash
sudo apt-get install ./package-name.deb
```

Or using dpkg directly:

```bash
sudo dpkg -i pkg.deb
```

If dependencies fail:

```bash
sudo apt-get -f install
```

---

## Step 8: Remove a Package with DPKG

```bash
sudo dpkg -r pkg
```

Used only when APT is unavailable or broken.

---

## Validation Checklist

You can confidently:

* Explain the difference between APT and DPKG
* Inspect package metadata before installation
* Perform safe upgrades
* Recover from failed installs

---

## Common Production Mistakes

* Running upgrades blindly on critical systems
* Mixing manual installs with package-managed files
* Using `dpkg` instead of APT by default

Avoid these habits early.

---

## Rollback / Cleanup

If nginx was installed:

```bash
sudo apt-get remove nginx
```

System state restored.

---

## Outcome

You now understand **Linux package management at an operational level**.

This skill is foundational for:

* Base image creation
* Security patching
* CI/CD environments
* Cloud instance maintenance
