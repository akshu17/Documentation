# Maintaining Branches for Different Features (Feature Branch Workflow)

Feature branching is a Git workflow where **each feature is developed in its own branch**.
This keeps work isolated, easier to manage, and safe to review before merging.

---

## 🌱 1. Create a Separate Branch for Each Feature

Always create feature branches from a stable base branch:

* `main` (production-ready code), or
* `develop` (integration branch)

### Example

```bash
git checkout develop
git pull
git checkout -b feature/login-page
```

### Naming conventions

Use clear and descriptive names:

* `feature/user-auth`
* `feature/payment-integration`
* `feature/dashboard-ui`

---

## 🛠 2. Work Only on That Feature

Keep the branch focused on one feature:

* Make small, meaningful commits
* Avoid mixing unrelated changes

### Example commit messages

```
Add login form UI
Implement password validation
Fix login error handling
```

---

## 🔄 3. Keep the Branch Updated

Regularly sync with the base branch to reduce merge conflicts.

### Using merge

```bash
git checkout feature/login-page
git fetch origin
git merge develop
```

### Or using rebase (if your team prefers)

```bash
git rebase develop
```

---

## 🧪 4. Test and Review Before Merging

When development is complete:

1. Push the feature branch to remote
2. Open a pull request (PR)
3. Perform code review
4. Run tests and validations

---

## 🔀 5. Merge the Feature

After approval:

* Merge into the base branch (`develop` or `main`)
* Delete the feature branch

### Delete local branch

```bash
git branch -d feature/login-page
```

### Delete remote branch

```bash
git push origin --delete feature/login-page
```

---

## 🧹 6. Keep Branches Short-Lived

Best practice:

* Small, focused features
* Merge quickly after completion
* Avoid long-running branches (they cause conflicts)

---

## 🧭 Example Workflow Structure

```
main (production)
   |
develop (integration)
   |-- feature/login
   |-- feature/payment
   |-- feature/profile
```

Each feature branch is merged back and then deleted.

---

## ✅ Best Practices Summary

✔ One branch per feature
✔ Clear naming conventions
✔ Frequent commits
✔ Regular sync with base branch
✔ Pull request before merge
✔ Delete branches after merge
✔ Keep branches short-lived

---
