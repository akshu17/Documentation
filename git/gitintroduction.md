# Git – Introduction, Architecture, and Core Commands

---

## Introduction to Git

**Git** is a **distributed version control system (DVCS)** used to track changes in source code during software development.
It allows multiple developers to collaborate efficiently, manage versions, and maintain a complete history of changes.

### Features of Git
- Version control
- Collaboration support
- Tracks complete history
- Fast and reliable
- Supports branching and merging

---

## Git Architecture

Git works with three main areas:

### 1. Working Directory
- Where files are created and modified
- Changes are not yet tracked

### 2. Staging Area (Index)
- Stores files ready to be committed
- Acts as a checkpoint

### 3. Repository
- Stores committed changes permanently
- Maintains full project history

### Architecture Flow

Working Directory → Staging Area → Local Repository → Remote Repository

---

## Git Commands with Examples

---

## 1. git clone

### Definition
`git clone` is used to copy an existing remote repository to the local system.

### Syntax
```bash
git clone <repository_url>
```

### Example
```bash
git clone https://github.com/user/project.git
```

---

## 2. git add

### Definition
`git add` moves files from the working directory to the staging area.

### Syntax
```bash
git add <file_name>
git add .
```

### Example
```bash
git add index.html
git add .
```

---

## 3. git commit

### Definition
`git commit` saves the staged changes to the local repository with a message.

### Syntax
```bash
git commit -m "message"
```

### Example
```bash
git commit -m "Added login feature"
```

---

## 4. git push

### Definition
`git push` uploads local commits to the remote repository.

### Syntax
```bash
git push origin branch_name
```

### Example
```bash
git push origin main
```

---

## 5. git pull

### Definition
`git pull` downloads changes from the remote repository and merges them into the local branch.

### Syntax
```bash
git pull origin branch_name
```

### Example
```bash
git pull origin main
```

---

## Difference Between git push and git pull

| Command | Purpose |
|------|---------|
| git push | Sends local changes to remote |
| git pull | Fetches remote changes to local |

---

## Complete Git Workflow Example

```bash
git clone https://github.com/user/project.git
cd project
git add .
git commit -m "Initial commit"
git push origin main
```

To update local repository:
```bash
git pull origin main
```

---

## Summary

- Git is a version control system
- Architecture includes Working Directory, Staging Area, and Repository
- clone copies repository
- add stages files
- commit saves changes
- push uploads changes
- pull downloads updates
