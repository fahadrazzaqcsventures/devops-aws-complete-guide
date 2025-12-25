# Environment Variables and Shell – Hands-On Lab

## Objective

Build **practical confidence** working with environment variables and shell behavior exactly as required in production systems.

By the end of this lab, you will:

* Inspect environment variables
* Create and export variables correctly
* Understand command resolution
* Customize shell behavior safely

---

## Lab Environment

* OS: Ubuntu Server 22.04
* Shell: bash
* User: Non-root user
* No GUI

---

## Step 1: View Environment Variables

```bash
env
```

Observe:

* Common variables like `HOME`, `PATH`, `USER`
* Large environments on real systems

---

## Step 2: Inspect a Variable

```bash
echo $HOME
echo $PATH
```

Understand:

* Variable expansion happens before execution
* Unset variables return empty output

---

## Step 3: Create a Shell Variable

```bash
MY_VAR="hello"
echo $MY_VAR
```

Test inheritance:

```bash
bash
echo $MY_VAR
```

Result:

* Variable is **not inherited**

Exit subshell:

```bash
exit
```

---

## Step 4: Export an Environment Variable

```bash
export MY_VAR="hello"
bash
echo $MY_VAR
```

Confirm:

* Exported variables propagate to child processes

---

## Step 5: Locate Command Binaries

```bash
which ls
which bash
```

Understand:

* Commands resolve via `PATH`
* First match wins

---

## Step 6: View Command History

```bash
history
```

Observe:

* Commands are stored sequentially
* Useful for audits and recovery

---

## Step 7: Create an Alias

```bash
alias ll='ls -la'
ll
```

Confirm:

* Alias expands before command execution

---

## Step 8: Remove an Alias

```bash
unalias ll
```

Validate:

```bash
ll
```

Expected:

* Command not found

---

## Validation Checklist

You can confidently:

* Explain environment variable inheritance
* Export variables intentionally
* Diagnose PATH-related issues
* Use aliases without breaking automation

---

## Common Production Mistakes

* Forgetting to export variables
* Relying on aliases in scripts
* Exposing secrets via history
* Modifying PATH incorrectly

---

## Rollback / Cleanup

```bash
unset MY_VAR
unalias ll 2>/dev/null
```

Session restored.

---

## Outcome

You now understand **shell behavior and environment control**.

This skill directly supports:

* Shell scripting
* CI/CD pipelines
* Docker and Kubernetes
* Cloud CLI tooling
