# Git – Revert vs Reset (Detailed Explanation with Examples)

---

## Introduction

In Git, **undoing changes** can be done using `git revert` or `git reset`.
Although both are used to undo commits, they work in very different ways and are used in different situations.

---

## Git Reset

### What is git reset?

`git reset` moves the **HEAD and branch pointer** to a previous commit.
It can remove commits from history and may delete changes.

⚠️ It **rewrites history**, so it is not safe for shared branches.

---

## Types of git reset

### 1. git reset --soft

- Removes commit
- Keeps changes in staging area
- Code is safe

```bash
git reset --soft HEAD~1
```

**Use case:** Edit commit message or add more files.

---

### 2. git reset --mixed (default)

- Removes commit
- Clears staging area
- Keeps changes in working directory

```bash
git reset HEAD~1
```

---

### 3. git reset --hard

- Removes commit
- Deletes all changes
- Data is permanently lost

```bash
git reset --hard HEAD~1
```

⚠️ Dangerous command.

---

## Example of git reset

```bash
git log
git reset --hard HEAD~1
```

---

## Git Revert

### What is git revert?

`git revert` undoes a commit by creating a **new commit** that reverses the changes.
It does not remove commit history.

✅ Safe for shared branches.

---

## How git revert works

- Original commit remains
- New commit reverses the changes
- History stays intact

---

## git revert command

```bash
git revert <commit_hash>
```

### Example

```bash
git revert a1b2c3d
```

---

## Revert latest commit

```bash
git revert HEAD
```

---

## Revert without opening editor

```bash
git revert --no-edit HEAD
```

---

## Revert example (after push)

```bash
git revert HEAD
git push origin main
```

---

## Difference Between git revert and git reset

| Feature | git reset | git revert |
|------|----------|-----------|
| Rewrites history | Yes | No |
| Creates new commit | No | Yes |
| Safe for shared branch | No | Yes |
| After push | Not recommended | Recommended |
| Risk | High | Low |

---

## When to use what?

### Use git reset when:
- Commit is local
- You haven't pushed
- Cleaning up history

### Use git revert when:
- Commit is pushed
- Working in a team
- Need safe undo

---

## Simple Rule

> Public branch → use git revert  
> Local commit only → use git reset

---

## Summary

- git reset removes commits
- git revert reverses commits
- Reset rewrites history
- Revert preserves history
- Revert is safer

---
