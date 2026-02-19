# git diff-tree — Markdown Notes

## What is `git diff-tree`?

`git diff-tree` is a Git command used to **compare a commit with its parent commit** and display what changes were introduced.

It shows:

* files changed
* additions
* deletions
* commit differences

---

## Why is `git diff-tree` Used?

* Inspect changes made in a specific commit
* Analyze commit history
* Automate change detection in scripts
* Used in Git hooks and CI/CD pipelines

---

## Basic Syntax

```bash
git diff-tree <commit>
```

This compares the given commit with its parent.

---

## Common Commands

### Show changed files in a commit

```bash
git diff-tree --name-only -r <commit>
```

---

### Show full changes (patch output)

```bash
git diff-tree -p <commit>
```

---

### Compare two commits

```bash
git diff-tree <commit1> <commit2>
```

---

## Important Options

| Option        | Meaning                                  |
| ------------- | ---------------------------------------- |
| `-r`          | Check changes recursively in directories |
| `--name-only` | Show only file names                     |
| `-p`          | Show detailed patch output               |

---

## Difference Between git diff and git diff-tree

| Command       | Purpose                                             |
| ------------- | --------------------------------------------------- |
| git diff      | Compare working directory, staging area, or commits |
| git diff-tree | Compare a commit with its parent                    |

---

## Real-World Usage

* Automated deployment checks
* Detect changed files in a commit
* CI/CD workflows
* Git hook scripting

---

## One-Line Summary

`git diff-tree` shows the differences introduced by a specific commit compared to its parent commit.
