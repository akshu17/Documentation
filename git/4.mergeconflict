# Merge Conflict in Git — Explanation & Resolution Guide

A **merge conflict** happens when Git cannot automatically combine changes from two branches because the **same part of a file was modified differently**.

Git stops the merge and asks you to manually decide which changes should remain.

---

## ⚠️ When Do Merge Conflicts Happen?

Common scenarios:

* Two developers edit the **same line** in the same file
* One branch deletes a file while another modifies it
* Your branch is outdated before merging
* Long-running feature branches diverge significantly

---

## 🧪 Example Scenario

### Branch `develop`

```js
let tax = 5;
```

### Branch `feature/payment`

```js
let tax = 10;
```

When merging → Git cannot decide which value is correct → conflict.

---

## 🔍 What a Merge Conflict Looks Like

Git marks the conflict directly in the file:

```js
<<<<<<< HEAD
let tax = 5;
=======
let tax = 10;
>>>>>>> feature/payment
```

Meaning:

* `<<<<<<< HEAD` → current branch version
* `=======` → separator
* `>>>>>>> feature/payment` → incoming branch version

You must edit the file manually.

---

## 🛠 How to Resolve a Merge Conflict (Step-by-Step)

### ✅ Step 1 — Attempt the merge

```bash
git merge feature/payment
```

Git stops and reports the conflict.

---

### ✅ Step 2 — Open the conflicted file

Look for the conflict markers:

```
<<<<<<<
=======
>>>>>>>
```

---

### ✅ Step 3 — Decide the final code

You can:

* Keep current version
* Keep incoming version
* Combine both
* Rewrite the logic

Example resolved file:

```js
let tax = 8;  // final agreed value
```

Remove all conflict markers.

---

### ✅ Step 4 — Mark the file as resolved

```bash
git add tax.js
```

---

### ✅ Step 5 — Complete the merge

```bash
git commit
```

Merge is now finished.

---

## 📌 Quick Command Summary

```bash
git merge branch-name
# fix conflicts manually
git add file-name
git commit
```

---

## 🔄 Merge vs Rebase Conflict Resolution

Conflicts can occur in both merge and rebase.

| Operation | What to run after fixing |
| --------- | ------------------------ |
| Merge     | `git commit`             |
| Rebase    | `git rebase --continue`  |

Resolution process is the same:

1. Fix file
2. Stage file
3. Continue process

---

## 🧠 Real Team Workflow

1. Two developers change the same file
2. One merges successfully
3. Second developer gets conflict
4. They update branch, fix conflict, commit

---

## 🚀 How to Avoid Merge Conflicts

* Pull latest changes before starting work
* Merge or rebase frequently
* Keep feature branches short-lived
* Communicate when editing shared files
* Make small, focused commits
* Use clear code ownership

---

## 💡 Simple Mental Model

Merge conflict =
**Two people changed the same thing differently → You decide the final version.**

---
