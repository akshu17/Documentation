# Check Difference Between Previous and Current Commit in Git

This guide explains how to compare changes between commits using Git.

---

## Compare Current Commit with Previous Commit

```bash
git diff HEAD~1 HEAD
```

### Explanation

* `HEAD` → current (latest) commit
* `HEAD~1` → previous commit

This command shows all changes introduced in the most recent commit.

---

## Shortcut Command

```bash
git diff HEAD~1
```

Git automatically compares the previous commit with the current commit.

---

## Compare Any Two Specific Commits

```bash
git diff <commit1> <commit2>
```

Example:

```bash
git diff a1b2c3 d4e5f6
```

Shows differences between two specific commit IDs.

---

## Show Only File Names That Changed

```bash
git diff --name-only HEAD~1 HEAD
```

Displays only the list of modified files.

---

## Show Summary of Changes

```bash
git diff --stat HEAD~1 HEAD
```

Displays:

* Number of files changed
* Insertions
* Deletions

---

## Compare Staged Changes with Last Commit

```bash
git diff --staged
```

or

```bash
git diff --cached
```

Shows changes that are staged but not yet committed.

---

## Most Common Command (Real Usage)

```bash
git diff HEAD~1 HEAD
```

Used to check what changed in the latest commit.

---

## Quick Summary

| Command                      | Purpose                             |
| ---------------------------- | ----------------------------------- |
| git diff HEAD~1 HEAD         | Compare previous and current commit |
| git diff HEAD~1              | Shortcut comparison                 |
| git diff <commit1> <commit2> | Compare any two commits             |
| git diff --name-only         | Show changed file names             |
| git diff --stat              | Show summary of changes             |
| git diff --staged            | Compare staged vs last commit       |

---

## One-Line Explanation

Use `git diff HEAD~1 HEAD` to see what changed between the previous and current com
