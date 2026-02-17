# 🧺 git stash drop

`git stash drop` is a Git command used to **delete a saved stash**.

------------------------------------------------------------------------

## ✅ What is a stash?

A stash is temporary storage where Git saves your uncommitted changes so
you can switch branches or work on something else without committing.

------------------------------------------------------------------------

## 🗑 What does `git stash drop` do?

It removes a specific stash entry from the stash list permanently.

Once dropped → you usually cannot recover it.

------------------------------------------------------------------------

## 🔹 Basic Syntax

``` bash
git stash drop stash@{n}
```

-   `stash@{n}` → the stash you want to delete\
-   `n` is the stash number

------------------------------------------------------------------------

## 🔹 Example

### 1️⃣ View all stashes

``` bash
git stash list
```

Example output:

    stash@{0}: WIP on main
    stash@{1}: WIP on feature

------------------------------------------------------------------------

### 2️⃣ Delete one stash

``` bash
git stash drop stash@{1}
```

This deletes the second stash.

------------------------------------------------------------------------

## 🔹 Delete the latest stash (shortcut)

If you don't specify anything, Git removes the most recent stash:

``` bash
git stash drop
```

Same as:

``` bash
git stash drop stash@{0}
```

------------------------------------------------------------------------

## 🔹 Delete ALL stashes (different command)

To remove everything:

``` bash
git stash clear
```

⚠️ This deletes all stashes permanently.

------------------------------------------------------------------------

## 🧠 Summary

-   `git stash drop` → delete one stash\
-   `git stash clear` → delete all stashes\
-   Dropped stashes are usually not recoverable
