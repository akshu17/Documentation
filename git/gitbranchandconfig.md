# Git – Branch and Config (Detailed with Examples)

---

## Git Branch

### What is a Branch in Git?

A **branch** in Git is a separate line of development that allows you to work on features, bug fixes, or experiments without affecting the main codebase.

By default, Git creates a branch named **main** (or **master** in older versions).

---

## Why Use Branches?

- Parallel development
- Safe experimentation
- Better collaboration
- Easy feature isolation

---

## Types of Branches

- **Main branch** – Production-ready code
- **Feature branch** – New features
- **Bug-fix branch** – Fixing issues
- **Release branch** – Preparing for release

---

## Git Branch Commands with Examples

### View All Branches
```bash
git branch
```

---

### Create a New Branch
```bash
git branch feature-login
```

---

### Switch to a Branch
```bash
git checkout feature-login
```
or
```bash
git switch feature-login
```

---

### Create and Switch Branch (Shortcut)
```bash
git checkout -b feature-payment
```

---

### Merge a Branch
```bash
git checkout main
git merge feature-payment
```

---

### Delete a Branch
```bash
git branch -d feature-payment
```

---

## Example Branch Workflow

```bash
git checkout -b feature-profile
# make changes
git add .
git commit -m "Added profile feature"
git checkout main
git merge feature-profile
```

---

## Git Config

### What is Git Config?

`git config` is used to configure Git settings such as username, email, editor, and aliases.
These settings define how Git behaves.

---

## Levels of Git Configuration

| Level | Scope |
|------|------|
| system | All users |
| global | Current user |
| local | Current repository |

---

## Common Git Config Commands

### Set Username
```bash
git config --global user.name "John Doe"
```

---

### Set Email
```bash
git config --global user.email "john@example.com"
```

---

### View All Configurations
```bash
git config --list
```

---

### View Specific Config Value
```bash
git config user.name
```

---

### Set Default Editor
```bash
git config --global core.editor "code --wait"
```

---

### Create Git Aliases

```bash
git config --global alias.st status
git config --global alias.cm commit
```

Usage:
```bash
git st
git cm -m "message"
```

---

## Difference Between Git Branch and Git Config

| Feature | Branch | Config |
|------|-------|--------|
| Purpose | Parallel development | Git settings |
| Scope | Repository | System/User/Repo |
| Affects | Code versions | Git behavior |

---

## Summary

- Branches allow parallel development
- Merging combines branch changes
- git config manages Git settings
- User name and email are mandatory
- Aliases improve productivity

---
