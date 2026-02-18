# Git — Detailed Interview Q&A

Comprehensive, detailed answers to common Git interview questions. Each answer provides in-depth context, examples, and best practices.

---

## 1. Git Branching Strategies

**What are the main Git branching strategies?**

Git branching strategies define how teams organize, create, and manage branches throughout development and release cycles. The major strategies include:

### Gitflow
- **Structure:** Multiple long-lived branches: `main`, `develop`, `feature/*`, `release/*`, `hotfix/*`
- **Use Case:** Large projects with scheduled releases, formal release management
- **Flow:** 
  - Features branch from `develop`
  - Release branches created from `develop` for final testing
  - Hotfixes branch from `main` for production bugs
  - All merges back to `main` and `develop`
- **Pros:** Clear structure, supports multiple versions
- **Cons:** Complex, many branches, slower for continuous delivery

### GitHub Flow
- **Structure:** `main` branch + short-lived feature branches
- **Use Case:** Continuous delivery, rapid deployment, small teams
- **Flow:**
  - Create feature branch from `main`
  - Work and push regularly
  - Open PR for code review
  - Merge to `main` after approval
  - Deploy immediately
- **Pros:** Simple, fast, CI/CD friendly
- **Cons:** Less formal, all releases from single branch

### Trunk-Based Development
- **Structure:** Single `main` branch with short-lived feature branches (< 24hrs)
- **Use Case:** High-velocity teams, continuous integration
- **Flow:**
  - Small, frequent commits to `main`
  - Feature flags for incomplete features
  - Immediate deployment
- **Pros:** Minimal merge conflicts, continuous delivery, rapid feedback
- **Cons:** Requires discipline, strong testing culture

### Forking Workflow
- **Structure:** Each contributor forks the repo, submits PRs to main repo
- **Use Case:** Open-source projects, distributed teams
- **Flow:** Fork → Clone → Branch → Push → PR → Review → Merge
- **Pros:** Decentralized, safe for untrusted contributors
- **Cons:** More overhead, slower approval process

**Choice Criteria:**
- Team size and structure
- Release frequency (continuous vs. scheduled)
- Project complexity
- Organizational maturity

---

## 2. From Which Branch You Release to Prod

**How do you determine the release branch for production?**

Production releases depend on your branching strategy and deployment model:

### Continuous Deployment
- Release directly from `main` branch
- Every merge to `main` triggers automated deployment
- Requires strong CI/CD and automated testing
- Suitable for GitHub Flow and Trunk-Based strategies

### Scheduled Releases
- Create `release/*` branches from `develop` (Gitflow)
- Example: `release/v1.2.0` created when ready for release
- Final testing and bug fixes happen here
- Merge to both `main` and `develop` after release
- Tag the release on `main` (e.g., `v1.2.0`)

### Long-Term Support (LTS)
- Maintain `release/v1.x`, `release/v2.x` branches for multiple versions
- Backport critical fixes to older versions
- Each version has its own release timeline

### Production Stabilization Branch
- Some teams use `production` or `stable` branch separate from `main`
- `main` = development, `production` = what's live
- Hot-fix directly to `production`, then backport to `main`

**Best Practices:**
- Always tag releases: `git tag -a v1.2.0 -m "Release v1.2.0"`
- Maintain CHANGELOG documenting each release
- Automate deployment from stable branches
- Never release from `develop` or feature branches

---

## 3. How You Maintain Branches for Different Features

**What's the lifecycle of a feature branch?**

Feature branch management ensures organized development and clean history:

### Creating Feature Branches
```bash
# Create from latest develop (Gitflow)
git checkout develop
git pull origin develop
git checkout -b feature/user-authentication

# Or from main (GitHub Flow)
git checkout main
git pull origin main
git checkout -b feature/user-authentication
```

### Naming Conventions
- `feature/user-authentication` - new features
- `bugfix/login-redirect-issue` - bug fixes
- `hotfix/security-vulnerability` - urgent production fixes
- `chore/update-dependencies` - maintenance tasks
- `docs/api-documentation` - documentation updates

### Development Workflow
1. **Frequent Commits:** Small, logical commits with clear messages
2. **Keep Updated:** Regularly sync with parent branch
   ```bash
   git fetch origin
   git rebase origin/develop  # or git merge if team prefers
   ```
3. **Push Regularly:** Daily pushes prevent work loss
   ```bash
   git push origin feature/user-authentication
   ```

### Code Review via PR
- Open PR as soon as there's working code
- Link to issue tracker (GitHub, Jira, etc.)
- Request specific reviewers
- Address feedback and push updates
- Rebase and squash commits if needed

### Merging
```bash
# Squash commits for cleaner history
git merge --squash feature/user-authentication

# Or keep history
git merge --no-ff feature/user-authentication

# Clean up after merge
git branch -d feature/user-authentication
git push origin --delete feature/user-authentication
```

### Best Practices
- Keep branches short-lived (< 1 week ideally)
- One feature per branch
- Regular syncing prevents large conflicts
- Delete merged branches immediately
- Use branch protection rules on main/develop

---

## 4. Merge Conflict? How You Resolve It?

**What causes merge conflicts and how do you resolve them?**

Merge conflicts occur when Git cannot automatically merge changes from different branches.

### When Conflicts Occur
- Same lines modified in different branches
- File deleted in one branch, modified in another
- Same file renamed differently
- Incompatible changes to the same code section

### Identifying Conflicts
```bash
git merge feature-branch
# OR
git rebase develop
# Results in:
# CONFLICT (content): Merge conflict in src/app.js
```

### Conflict Markers
Git marks conflicting sections:
```javascript
<<<<<<< HEAD (current branch)
const apiUrl = 'http://localhost:3000';
=======
const apiUrl = 'http://api.production.com';
>>>>>>> feature/api-endpoint
```

### Resolution Steps

**Step 1: Identify All Conflicts**
```bash
git status                    # Shows conflicted files
git diff                      # Shows all conflicts
grep -r "<<<<<<< HEAD" .      # Find all conflict markers
```

**Step 2: Resolve Manually**
- Open each conflicted file
- Review both versions
- Choose which change to keep or combine both
- Remove conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)

**Step 3: Test Resolution**
```bash
# Test the resolved code
npm test
# or
python -m pytest
# or your test suite
```

**Step 4: Complete Merge**
```bash
# Mark files as resolved
git add src/app.js
git add src/config.js

# For merge
git commit -m "Resolve merge conflicts in API configuration"

# For rebase
git rebase --continue
```

### Conflict Resolution Strategies

**Ours (Keep Current Branch)**
```bash
git checkout --ours src/app.js
git add src/app.js
```

**Theirs (Keep Incoming Branch)**
```bash
git checkout --theirs src/app.js
git add src/app.js
```

**Use Merge Tools**
```bash
git mergetool                  # Interactive conflict resolution
# Opens configured tool (VSCode, Vimdiff, etc.)
```

### Tools & IDE Support
- **VSCode:** Built-in merge conflict UI (Accept Current/Incoming/Both)
- **JetBrains IDEs:** Integrated conflict resolver
- **Terminal:** `git mergetool` with custom tools

### Preventing Conflicts
- Communicate with team members
- Keep feature branches short-lived
- Regular merges from parent branch
- Separate concerns (different files/modules)
- Code reviews before merge

### Complex Conflict Scenario
```bash
# If you get stuck
git merge --abort              # Cancel merge
git rebase --abort             # Cancel rebase

# Start over and try different approach
git reset --hard origin/develop
```

---

## 5. PR Approval Process?

**Explain the pull request approval and merge workflow**

A PR (Pull Request) is the gatekeeper for code quality, ensuring reviewed and tested code reaches production.

### PR Lifecycle

**1. Creating PR**
```bash
# Push feature branch
git push origin feature/payment-integration

# Then create PR on GitHub/GitLab/Bitbucket UI
# OR via CLI
gh pr create --title "Add payment integration" --body "Implements Stripe integration"
```

**2. PR Description**
- Clear title: "Fix: Correct user login redirect" or "Feature: Add payment processing"
- Detailed description:
  - What problem does this solve?
  - How does it work?
  - Testing performed
  - Screenshots/videos if relevant
  - Closes issue #123

**3. CI/CD Checks Run Automatically**
- Unit tests must pass
- Linting checks
- Code coverage targets
- Security scanning
- Build verification
- Deployment preview (staging environment)

**4. Code Review Assignment**
- Select reviewers (team leads, subject matter experts)
- Assign specific reviewers or use automatic assignment
- Set minimum required approvals (e.g., 2 approvals)
- Assign to yourself for final review

**5. Review Process**
Reviewers check:
- Code logic and correctness
- Design patterns and consistency
- Performance implications
- Security vulnerabilities
- Test coverage
- Documentation updates

**Reviewer Actions:**
```
- Comment: General discussion
- Approve: Code is good to merge
- Request Changes: Must fix issues before merge
```

**6. Addressing Feedback**
```bash
# Make changes locally
git add file.js
git commit -m "Address review feedback: improve error handling"
git push origin feature/payment-integration

# Conversation continues, dismiss outdated comments
# Re-request review after fixes
```

**7. Final Checks Before Merge**
- All CI checks pass ✓
- All conversations resolved ✓
- Required approvals obtained ✓
- Branch is up-to-date with main ✓
- No conflicts ✓

**8. Merge to Main**
```bash
# Option 1: Squash commits (clean history)
git merge --squash feature/payment-integration

# Option 2: Create merge commit (preserve history)
git merge --no-ff feature/payment-integration

# Option 3: Rebase and fast-forward
git rebase origin/main
git merge --ff feature/payment-integration

# Delete branch after merge
git branch -d feature/payment-integration
git push origin --delete feature/payment-integration
```

**9. Deployment**
- Merge to `main` triggers deployment to staging
- After staging verification, auto-deploy to production
- Or manual approval required for production

### PR Best Practices
- Keep PRs focused and small (< 400 lines is ideal)
- Title should be clear and descriptive
- Link to related issues
- Include testing instructions
- Request review immediately after PR creation
- Respond to feedback promptly
- Don't force-push after review starts (loses context)

### Common PR Policies
- Minimum 2 approvals
- At least one approval from maintainer/team lead
- No self-approval
- All conversations must be resolved
- Automatic stale PR closure (after 30 days)
- Branch must be updated before merge

---

## 6. Diff Between `git pull` and `git fetch`

**What's the difference between pull and fetch, and when do you use each?**

Both download remote changes, but they work differently and serve different purposes.

### `git fetch`
**What it does:**
- Downloads new commits, branches, and tags from remote repository
- Updates remote-tracking branches (e.g., `origin/main`)
- Does NOT change your working tree or local branches
- Safe operation with no side effects

**Command:**
```bash
git fetch origin                # Fetch from origin remote
git fetch                       # Fetch from all remotes
git fetch origin main           # Fetch specific branch
git fetch --all                 # Fetch from all remotes
git fetch --prune              # Remove deleted remote branches locally
```

**Result:**
```bash
# Before fetch
Local main: commit ABC
Remote origin/main: commit XYZ

# After fetch
Local main: commit ABC (unchanged)
Remote origin/main: commit XYZ (updated locally)
```

**When to use:**
- Review remote changes before integrating
- Compare local vs remote versions
- Prepare for merge without applying it
- Update multiple branches simultaneously
- Safe exploration of remote work

### `git pull`
**What it does:**
- Downloads commits from remote (like fetch)
- Automatically integrates changes into current branch
- Equivalent to: `git fetch` + `git merge` or `git rebase`
- Modifies your working tree

**Command:**
```bash
git pull origin main            # Fetch and merge
git pull --rebase              # Fetch and rebase (linear history)
git pull origin                # Fetch and merge from default branch
```

**Result:**
```bash
# Before pull
Local main: commit ABC
Remote origin/main: commit XYZ

# After pull with merge
Local main: commit MERGE (merges ABC and XYZ)

# After pull with rebase
Local main: commit XYZ (rebased, ABC moved on top)
```

### Side-by-Side Comparison

| Aspect | `git fetch` | `git pull` |
|--------|------------|-----------|
| Downloads changes | ✓ | ✓ |
| Integrates changes | ✗ | ✓ |
| Creates merge commit | ✗ | ✓ (default) |
| Can rebase | ✗ | ✓ (with --rebase) |
| Modifies working tree | ✗ | ✓ |
| Safe to run | ✓ | ✓ (usually) |
| Workflow control | Manual | Automatic |

### Practical Workflow Examples

**Fetch + Review + Decide**
```bash
# Fetch updates
git fetch origin

# Compare local vs remote
git log main..origin/main          # Commits in remote not in local
git diff main origin/main          # Actual code changes

# Now decide to merge or rebase
git merge origin/main
# OR
git rebase origin/main
```

**Pull with Rebase (Recommended)**
```bash
# Get latest and rebase local work on top
git pull --rebase origin main

# If conflicts occur, resolve them:
git add .
git rebase --continue
```

**Pull for Collaborative Work**
```bash
# If working on shared branch with multiple contributors
git pull origin feature/shared-feature

# If you have unpublished commits, this creates merge commit
# (Better than rebase for shared/collaborative branches)
```

### Best Practice
```bash
# Configure pull to rebase by default (cleaner history)
git config --global pull.rebase true

# Or rebase for specific branch
git config branch.main.rebase true
```

### When Conflicts Occur
```bash
# During pull
git pull origin main
# Conflict! Auto-merge failed

# Option 1: Resolve and complete merge
# ... resolve conflicts ...
git add .
git commit

# Option 2: Try rebase instead
git pull --abort
git pull --rebase origin main
# ... resolve rebase conflicts ...
git rebase --continue
```

---

## 7. Branching Strategy (Summary)

**What is a branching strategy and why is it important?**

A branching strategy is a set of rules and conventions for how teams organize work using Git branches.

**Why It Matters:**
- Prevents chaos and merge conflicts
- Enables parallel development
- Supports multiple release versions
- Facilitates code review and quality
- Automates testing and deployment
- Clear communication about work status

**Choose Based On:**
1. **Release Frequency:** Continuous (GitHub Flow) vs. Scheduled (Gitflow)
2. **Team Size:** Small (GitHub Flow) vs. Large (Gitflow)
3. **Deployment Maturity:** High CI/CD (Trunk-Based) vs. Manual deployments (Gitflow)
4. **Project Complexity:** Single product (GitHub Flow) vs. Multiple versions (Gitflow)

---

## 8. Types of Branching Strategy

**What are the main branching strategy types?**

**1. Gitflow**
- Purpose: Formal release management
- Branches: `main`, `develop`, `feature/*`, `release/*`, `hotfix/*`
- Best for: Enterprise, scheduled releases, multiple versions

**2. GitHub Flow**
- Purpose: Continuous delivery
- Branches: `main`, `feature/*`
- Best for: SaaS, rapid deployment, small teams

**3. Trunk-Based Development**
- Purpose: Maximum collaboration, minimal branching
- Branches: `main`, short-lived `feature/*` (< 1 day)
- Best for: Microservices, DevOps, high velocity

**4. Forking Workflow**
- Purpose: Decentralized contributions
- Branches: Fork → Branch → PR
- Best for: Open-source, untrusted contributors

**5. Release Branching**
- Purpose: Support multiple production versions
- Branches: `main`, `release/v1.x`, `release/v2.x`
- Best for: Libraries, long-term support products

---

## 9. Which Branching Strategy You Are Using in Your Project

**Interview Answer Template:**

"In my current project, we use **GitHub Flow** because it aligns with our continuous delivery goals. Here's how it works:

- We maintain a single `main` branch that's always deployable
- Each feature/bug gets its own branch (e.g., `feature/user-auth`)
- Developers work on feature branches and push frequently
- When ready, they open a PR with description and testing notes
- Code review is required (minimum 2 approvals from team)
- All CI/CD checks must pass before merge
- After merge to `main`, automated deployment to staging happens immediately
- Following staging verification, auto-deployment to production

We chose this because:
1. Our team is small (4-5 developers) and communicates well
2. We deploy multiple times per week
3. It's simple to understand and reduces merge conflicts
4. Fits our DevOps/cloud-native infrastructure"

**Alternative answers based on strategy:**

For **Gitflow:**
"We use Gitflow for formal release cycles. We maintain `main` (production), `develop` (integration), feature branches, and release branches. Each sprint, features are created from `develop`, and at sprint end, we create a `release/` branch for testing and hotfixes..."

For **Trunk-Based:**
"We use trunk-based development to enable rapid iteration. We keep feature branches very short-lived (usually merged within 24 hours), use feature flags for incomplete work, and deploy multiple times daily..."

---

## 10. Some Basic Git Commands

**Essential Git commands every developer should know:**

### Setup & Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --global core.editor "vim"                    # Set default editor
git config --list                                        # View all config
```

### Cloning & Initialization
```bash
git clone <url>                                          # Clone remote repo
git clone <url> <directory>                             # Clone to specific folder
git init                                                # Initialize new repo
```

### Status & Inspection
```bash
git status                                              # Show working tree status
git log                                                 # Show commit history
git log --oneline                                       # Compact log
git log -p                                              # Show commits with diffs
git log --graph --oneline --all                        # Visual branch history
git show <commit>                                       # Show commit details
git diff                                                # Show unstaged changes
git diff --staged                                       # Show staged changes
git blame <file>                                        # Show who changed each line
```

### Branching
```bash
git branch                                              # List local branches
git branch -a                                           # List all branches
git branch <branch-name>                                # Create branch
git checkout <branch-name>                              # Switch branch
git checkout -b <branch-name>                           # Create and switch
git switch <branch-name>                                # Modern alternative
git switch -c <branch-name>                             # Create and switch (modern)
git branch -d <branch-name>                             # Delete branch
git branch -D <branch-name>                             # Force delete
git branch -m <old-name> <new-name>                    # Rename branch
git push origin --delete <branch-name>                 # Delete remote branch
```

### Staging & Committing
```bash
git add <file>                                          # Stage specific file
git add .                                               # Stage all changes
git add -p                                              # Interactive staging (hunks)
git commit -m "Commit message"                          # Commit with message
git commit --amend                                      # Modify last commit
git commit --amend --no-edit                            # Amend without changing message
git reset <file>                                        # Unstage file
git reset HEAD~1                                        # Undo last commit (keep changes)
git reset --hard HEAD~1                                 # Undo last commit (discard changes)
```

### Merging & Rebasing
```bash
git merge <branch-name>                                 # Merge branch into current
git merge --no-ff <branch-name>                         # Create merge commit always
git merge --squash <branch-name>                        # Squash commits before merge
git rebase <branch>                                     # Rebase onto another branch
git rebase -i HEAD~3                                    # Interactive rebase last 3 commits
git rebase --continue                                   # Continue after resolving conflicts
git rebase --abort                                      # Cancel rebase
```

### Remote Operations
```bash
git remote -v                                           # List remotes with URLs
git remote add <name> <url>                             # Add remote
git remote remove <name>                                # Remove remote
git fetch origin                                        # Fetch from remote
git pull origin <branch>                                # Fetch and merge
git push origin <branch>                                # Push to remote
git push origin --all                                   # Push all branches
git push origin <branch> --force                        # Force push (use carefully!)
git push origin --tags                                  # Push all tags
```

### Stashing
```bash
git stash                                               # Stash current changes
git stash list                                          # List stashes
git stash pop                                           # Apply and remove last stash
git stash apply stash@{0}                               # Apply specific stash
git stash drop stash@{0}                                # Delete specific stash
git stash clear                                         # Delete all stashes
```

### Tags
```bash
git tag <tag-name>                                      # Create lightweight tag
git tag -a <tag-name> -m "message"                     # Create annotated tag
git push origin <tag-name>                              # Push specific tag
git push origin --tags                                  # Push all tags
git tag -d <tag-name>                                   # Delete local tag
git push origin --delete <tag-name>                    # Delete remote tag
```

---

## 11. How Do You Change Git Remote URL to Local URL

**How do you change a remote repository URL, especially to a local path?**

### Viewing Current Remote
```bash
git remote -v                  # Shows all remotes with URLs
# Output:
# origin  https://github.com/user/repo.git (fetch)
# origin  https://github.com/user/repo.git (push)
```

### Changing Remote URL

**Method 1: Using `git remote set-url`**
```bash
# Change origin to a local path
git remote set-url origin /path/to/local/repository

# Change origin to HTTP
git remote set-url origin https://github.com/user/repo.git

# Change origin to SSH
git remote set-url origin git@github.com:user/repo.git

# Verify change
git remote -v
```

**Method 2: Edit `.git/config` Directly**
```bash
# Open .git/config in editor
vim .git/config

# Change the URL under [remote "origin"]
[remote "origin"]
    url = /path/to/local/repository    # Changed here
    fetch = +refs/heads/*:refs/remotes/origin/*
```

### Local Repository URL Examples
```bash
# Absolute path
git remote set-url origin /Users/username/repositories/my-project

# Relative path (if repos are in same parent folder)
git remote set-url origin ../other-project

# On Windows
git remote set-url origin C:\Users\username\repositories\my-project

# Using file protocol (not recommended but works)
git remote set-url origin file:///path/to/repository
```

### Practical Scenario
```bash
# Clone from GitHub initially
git clone https://github.com/user/repo.git my-project

# Work for a while, then switch to local mirror
cd my-project
git remote set-url origin /Users/local-mirror/repo

# Now push/pull from local instead
git push origin main
git pull origin main
```

### Multiple Remotes
```bash
# You can have multiple remotes
git remote add upstream https://github.com/original/repo.git
git remote add local /path/to/local/repo

# Fetch/pull from different remotes
git fetch upstream
git pull local main
git push origin feature/my-feature
```

### Troubleshooting
```bash
# If URL is wrong, try resetting
git remote remove origin
git remote add origin /new/path/to/repo

# Or try with absolute path if relative doesn't work
git remote set-url origin /absolute/path/to/repo

# Test connection
git fetch origin --dry-run
```

---

## 12. Git Architecture

**Explain the architecture and internal structure of Git**

Git's architecture is based on a distributed object database model:

### Core Components

**1. Git Objects**
Git stores everything in a content-addressable filesystem:

- **Blob (Binary Large Object):** Raw file content
  ```
  Type: blob
  Size: 1234 bytes
  SHA-1: abc123def456...
  ```

- **Tree:** Directory structure, points to blobs and other trees
  ```
  tree 789def
    blob abc123 file.txt
    blob def456 config.json
    tree 456ghi subfolder/
  ```

- **Commit:** Snapshot of repository state
  ```
  commit abc123
    Tree: 789def
    Parent: prev-commit-sha
    Author: Name <email>
    Message: "Add feature X"
  ```

- **Tag:** Named reference to a commit (for releases)
  ```
  tag v1.0.0
    Object: abc123 (commit)
    Message: "Release version 1.0.0"
  ```

**2. References (Refs)**
- **Branches:** Pointers to commits (movable refs)
  - Stored in `.git/refs/heads/main`
  - Contains SHA-1 of current commit
  
- **HEAD:** Current branch pointer
  - Stored in `.git/HEAD`
  - Usually points to current branch
  
- **Tags:** Permanent references to commits
  - Stored in `.git/refs/tags/`
  - Don't move unlike branches

**3. Index (Staging Area)**
- `.git/index` file
- Records which files are staged
- Acts as intermediate between working tree and repository
- Allows selective commits

**4. Working Tree**
- Actual files and directories you edit
- Extracted from Git objects when needed
- Temporary view of a commit's content

**5. Local Repository**
- `.git/` directory
- Contains all Git objects, refs, config
- Full history and branching information
- Can work completely offline

### Three-Stage Architecture

```
┌─────────────────────────────────────────┐
│         Remote Repository               │
│      (GitHub, GitLab, server)           │
└──────────┬──────────────────────────────┘
           │ git fetch / git push
┌──────────▼──────────────────────────────┐
│       Local Repository (.git/)          │
│  - Objects (blobs, trees, commits)      │
│  - Refs (branches, tags, HEAD)          │
│  - Logs and history                     │
└──────────┬──────────────────────────────┘
           │ git checkout / git add
┌──────────▼──────────────────────────────┐
│            Index (Staging)              │
│  - Tracks which files to commit         │
└──────────┬──────────────────────────────┘
           │ git add / git commit
┌──────────▼──────────────────────────────┐
│         Working Directory               │
│   - Your actual files and folders       │
│   - Where you make edits                │
└─────────────────────────────────────────┘
```

### Workflow Through Architecture

```bash
# 1. Edit files (in Working Tree)
echo "new code" >> file.js

# 2. Stage changes (copy to Index)
git add file.js

# 3. Commit (create objects in Repository)
git commit -m "Add feature"
# - Creates Blob for file.js content
# - Creates Tree for directory structure
# - Creates Commit pointing to Tree
# - Updates Branch ref to new Commit

# 4. Push (send to Remote Repository)
git push origin main
```

### Storage Efficiency

**Packfiles:**
- Git combines multiple objects into `.pack` files
- Compresses and deduplicates data
- Triggered by `git gc` or during push
- Significantly reduces disk space

**Delta Encoding:**
- Stores only differences between similar files
- Full file (delta base) + changes for others
- Reduces repository size 70-90%

### Distributed Nature

Each clone contains:
- Full commit history (all branches, tags)
- Complete object database
- All refs and configurations
- Independent from network

Allows:
- Complete offline work
- Local branching and merging
- Independent repository copies
- Decentralized collaboration

### Configuration Files

```
.git/
├── config                  # Local repo config
├── HEAD                    # Current branch pointer
├── index                   # Staging area
├── objects/                # Git objects (blobs, trees, commits)
├── refs/
│   ├── heads/             # Local branch pointers
│   ├── remotes/           # Remote branch pointers
│   └── tags/              # Tag references
├── logs/                   # Reflog and histories
├── hooks/                  # Git hooks scripts
└── info/
    └── exclude            # Local gitignore
```

---

## 13. Explain Branching Strategy (Detailed)

**Provide a comprehensive explanation of branching strategies**

[See questions #1 and #7 for detailed branching strategy explanations]

### Implementation in Real Project

Suppose we're implementing GitHub Flow:

**1. Main Branch Protection**
- No direct commits to `main`
- All changes via PR only
- Require PR reviews before merge
- Require all status checks pass
- Dismiss stale PR approvals when new commits pushed

**2. Feature Branch Workflow**
```bash
# Developer starts feature
git checkout -b feature/dark-mode

# Regular commits during development
git commit -m "Add dark mode toggle"
git commit -m "Style dark theme"
git push origin feature/dark-mode

# After a few commits, open PR on GitHub
# Set reviewer and link to issue #42

# Reviewer comments, requests changes
# Developer makes fixes
git commit -m "Address review: improve contrast ratios"
git push origin feature/dark-mode

# After approval, merge
# GitHub closes PR and deletes branch

# Locally clean up
git fetch -p                           # Prune deleted branches
git checkout main
git pull origin main
git branch -d feature/dark-mode
```

**3. Multiple Concurrent Features**
```bash
# Team has 4 features in progress simultaneously
# Each on separate branch from main
# Code review gates ensure quality
# No conflicts because branches don't overlap
# Main always stays production-ready
```

**4. Emergency Hotfix**
```bash
# Production bug found!
git checkout -b hotfix/critical-security-bug

# Fix and test
git commit -m "Security: Escape user input"
git push origin hotfix/critical-security-bug

# PR, review, merge immediately
# Bypass normal review if critical
# Also merge back to develop for Gitflow

git checkout main
git merge --no-ff hotfix/critical-security-bug
git tag v1.2.1
git push origin main v1.2.1
```

---

## 14. Git Fetch vs Git Pull (Detailed)

[See question #6 for comprehensive fetch vs pull explanation]

### Real-World Scenarios

**Scenario 1: Before Merging Remote Changes**
```bash
# Colleague pushed changes you haven't seen
git fetch origin                    # Download their work

# Review before merging
git log main..origin/main          # Their new commits
git diff main origin/main           # Actual changes

# Decide if you're comfortable merging
git merge origin/main              # If yes, merge
```

**Scenario 2: Multiple Collaborators**
```bash
# Three teammates work on shared branch
git fetch origin

# See 5 new commits from teammates
git log --oneline -5 origin/feature/shared

# Decide: merge or rebase?
git rebase origin/feature/shared    # Rebase local work
# OR
git merge origin/feature/shared     # Create merge commit

# Then continue work
```

**Scenario 3: Quick Update Before Push**
```bash
# Make several commits locally
git commit -m "Add feature"

# Before pushing, check for conflicts
git fetch origin
git diff main origin/main

# If no conflicts, safe to push
git push origin main
```

---

## 15. Git Merge vs Git Rebase (Detailed)

**Understand when to use merge vs rebase**

### `git merge`

**What It Does:**
- Combines two branches by creating a merge commit
- Preserves complete branch history
- Non-destructive operation

**Syntax:**
```bash
git merge <source-branch>
git merge --no-ff <branch>         # Force merge commit
git merge --squash <branch>        # Squash before merge
```

**Result:**
```
Before:
  main:        A---B---C
  feature:         D---E

After merge:
  main:        A---B---C---M (M = merge commit)
               |       \ /
  feature:         D---E

# Git log shows both branches' history
```

**Advantages:**
- Complete history preservation
- Easy to understand what happened
- Safe for shared branches
- Shows collaboration clearly

**Disadvantages:**
- Creates merge commits that clutter history
- History becomes non-linear
- Harder to track individual feature development
- More commits to review in history

### `git rebase`

**What It Does:**
- Replays commits from one branch onto another
- Rewrites commit history to be linear
- Makes history cleaner but modifies commit SHAs

**Syntax:**
```bash
git rebase <base-branch>
git rebase -i HEAD~3               # Interactive rebase
git rebase --continue              # After resolving conflicts
```

**Result:**
```
Before:
  main:        A---B---C
  feature:         D---E

After rebase:
  main:        A---B---C---D---E (all linear, D' and E' are new SHAs)

# Commits D and E are replayed on top of C
```

**Advantages:**
- Linear, clean history
- Easier to understand feature development
- Simpler `git log` output
- Easier to bisect for bug finding
- Less merge commit noise

**Disadvantages:**
- Rewrites history (breaks if commits are public)
- Commits get new SHAs (harder to track)
- More complex for shared branches
- Potential for losing commits if done wrong

### When to Use Each

**Use Merge When:**
- Working on shared/public branches
- Collaborating with multiple people
- Want to preserve branch history
- Creating release branches
- Formal integration point needed

```bash
# Merging feature into main for release
git checkout main
git merge --no-ff release/v1.2.0
```

**Use Rebase When:**
- Working on personal feature branch
- Before pushing to public branch
- Cleaning up local commits
- Linear history is important
- Want cleaner feature history

```bash
# Before pushing personal work
git rebase origin/main
git push origin feature/my-feature
```

### Combining Both: The Best Practice Workflow

```bash
# 1. Work on feature branch (many commits)
git checkout -b feature/dashboard
git commit -m "Create dashboard component"
git commit -m "Add styling"
git commit -m "Add tests"

# 2. Before pushing, rebase to clean up
git fetch origin
git rebase origin/main             # Linear history

# 3. Push to remote (now history is clean)
git push origin feature/dashboard

# 4. Open PR and get reviewed

# 5. After approval, merge into main
git checkout main
git merge --no-ff feature/dashboard # Preserves merge point

# 6. Delete feature branch
git branch -d feature/dashboard
```

### Interactive Rebase for Cleaning History

```bash
# Squash commits before merge
git rebase -i HEAD~3

# Interactive editor opens:
# pick abc123 Create dashboard
# pick def456 Add styling
# squash ghi789 Fix typo          # Squash this
# pick jkl012 Add tests

# Result: Only 3 commits in final merge
```

### Conflict Resolution in Rebase vs Merge

**Merge Conflict:**
```bash
git merge feature
# Conflict!
# Edit files
git add .
git commit              # Complete merge
```

**Rebase Conflict:**
```bash
git rebase main
# Conflict during replay of commit 1 of 3
# Edit files
git add .
git rebase --continue   # Continue replaying other commits
# May have conflicts in next commits too
```

---

## 16. Merge Conflict (Detailed)

[See question #4 for comprehensive merge conflict explanation]

### Advanced Conflict Scenarios

**Scenario 1: Conflict During Complex Rebase**
```bash
git rebase -i origin/main
# 3 commits to replay
# Conflict on commit 1 of 3

# Resolve first conflict
# ... edit files ...
git add .
git rebase --continue

# Conflict on commit 2 of 3
# ... edit files ...
git add .
git rebase --continue

# Success!
```

**Scenario 2: Merge Conflict in Binary Files**
```bash
# Can't resolve binary files manually
git status
# both modified: image.png

# Take their version
git checkout --theirs image.png
git add image.png
git commit

# Or keep ours
git checkout --ours image.png
```

**Scenario 3: Delete/Modify Conflict**
```bash
# You deleted file.js, teammate modified it
git merge feature
# Conflict!
# CONFLICT (delete/modify): file.js deleted in HEAD and modified in feature

# Keep deleted
git rm file.js

# Keep modified
git add file.js
```

---

## 17. Git Stash (Detailed)

**What is Git stash and how do you use it?**

Git stash temporarily saves uncommitted changes, allowing clean branch switching without committing.

### Basic Stash Operations

**Stashing Changes**
```bash
# Save current uncommitted changes
git stash                               # or git stash save

# Stash with descriptive message
git stash save "WIP: implementing auth feature"

# Stash only staged changes
git stash push --staged

# Stash specific file
git stash push src/app.js

# Stash including untracked files
git stash -u                            # -u or --include-untracked

# Stash all changes and staged
git stash --all                         # Includes ignored files
```

**Listing Stashes**
```bash
git stash list
# Output:
# stash@{0}: WIP on main: abc123 Last commit message
# stash@{1}: WIP on feature: def456 Previous commit
# stash@{2}: WIP on main: ghi789 Even older
```

**Applying Stashes**
```bash
# Apply most recent stash (keeps it)
git stash apply

# Apply specific stash
git stash apply stash@{1}

# Apply and remove (pop)
git stash pop                           # Removes stash@{0}
git stash pop stash@{1}                 # Apply and remove specific

# View stash before applying
git stash show                          # Show files in stash@{0}
git stash show -p                       # Show actual changes
git stash show stash@{1}                # Show specific stash
```

**Deleting Stashes**
```bash
# Delete most recent
git stash drop

# Delete specific stash
git stash drop stash@{1}

# Delete all stashes
git stash clear

# Safety: confirm before deleting
git stash list                          # Review first
```

### Real-World Stash Scenarios

**Scenario 1: Interrupted Work**
```bash
# Working on feature, not ready to commit
git status
# On branch feature/auth
# Changes not staged: src/auth.js, src/utils.js

# Urgent bug fix needed
git stash

# Switch to main, create hotfix
git checkout main
git checkout -b hotfix/critical-bug

# Fix and merge
# ... fix and test ...
git commit -m "Fix critical bug"
git push origin hotfix/critical-bug

# Back to feature work
git checkout feature/auth
git stash pop               # Restore work

# Continue editing
```

**Scenario 2: Try Different Approach**
```bash
# Attempt a solution
git stash save "First attempt at feature"

# Start fresh
git checkout -b feature/alt-approach

# Try different implementation
# ... code ...

# Compare approaches
git stash show stash@{0} -p             # View first attempt
# Decide which is better, continue with better one
```

**Scenario 3: Clean Working Tree**
```bash
# Need clean state for testing
git stash --all                         # Stash everything

# Test application
npm test

# Restore work
git stash pop
```

### Advanced Stash Operations

**Creating Branch from Stash**
```bash
# Useful if stash got lost or you need it as a branch
git stash branch feature/from-stash

# Creates new branch and applies stash
# Helpful if stash index changed
```

**Exporting Stash as Patch**
```bash
# Save stash as file
git stash show -p > my-changes.patch

# Send to teammate or archive
# Apply later
git apply my-changes.patch
```

**Checking for Stashed Changes**
```bash
# Before switching branches, check stash
git stash list | wc -l                  # Count stashes

# Dangerous: losing work
git stash drop stash@{10}               # Lost!

# Better: list what you're deleting
git stash show stash@{10} -p            # See changes first
```

---

## 18. About Version Control Tool

**Explain version control tools and their importance**

Version Control Systems (VCS) are software tools that manage changes to files over time, enabling collaboration and tracking history.

### What is Version Control?

**Core Functions:**
1. **History Tracking:** Maintain complete record of all changes
2. **Collaboration:** Enable multiple people to work simultaneously
3. **Branching:** Create parallel development lines
4. **Merging:** Integrate changes from different branches
5. **Reverting:** Undo changes if needed
6. **Auditing:** Track who changed what and why

### Types of Version Control

**Centralized VCS (CVCS)**
- Single central repository server
- Examples: SVN, Perforce
- Requires network connection
- Single point of failure

**Distributed VCS (DVCS)**
- Multiple copies of repository
- Examples: Git, Mercurial
- Works offline completely
- More resilient

### Why Git is Popular

**Advantages:**
- Distributed architecture (offline work, backups)
- Fast local operations (no server needed)
- Excellent branching and merging
- Large file support with Git LFS
- Strong community and ecosystem
- GitHub/GitLab platforms built on Git
- De facto standard for open source

**Disadvantages:**
- Steeper learning curve
- Large binaries bloat repository
- Complex history can be confusing
- Command-line has many options

### Version Control in Workflow

```
Developer writes code
    ↓
Stage changes (git add)
    ↓
Commit to local repo (git commit)
    ↓
Push to remote (git push)
    ↓
Create PR
    ↓
Code review
    ↓
Merge to main (git merge)
    ↓
Automated tests run
    ↓
Deploy to production
```

### Business Value

1. **Code Safety:** Complete backup of all versions
2. **Accountability:** Track author and timestamp of all changes
3. **Quality:** Code review gates prevent bad code
4. **Compliance:** Audit trail for regulations
5. **Incident Response:** Quickly revert bad deployments
6. **Team Collaboration:** Multiple developers work together
7. **Release Management:** Track versions and releases
8. **Documentation:** Commit messages explain changes

---

## 19. Git Stash Drop

**How to delete specific Git stashes**

See question #17 for comprehensive stash explanation. Here's stash drop specifically:

```bash
# Delete most recent stash
git stash drop                          # Removes stash@{0}

# Delete specific stash
git stash drop stash@{2}

# Delete all stashes at once
git stash clear

# Verify deletion
git stash list                          # Should be gone
```

**Safety Tips:**
```bash
# Before deleting, review what you're removing
git stash show stash@{2} -p
git stash show stash@{2}

# If accidentally deleted, recovery is very difficult
# Only delete when confident
```

---

## 20. How to Fix Broken Commit in Git

**Repair or modify commits that have errors**

### Recent Commit (Not Pushed)

**Fix the Most Recent Commit**
```bash
# Made typo in code or commit message
git commit -m "Fix bug in autentication module"

# Fix the code
# ... edit file ...
git add file.js

# Amend the commit
git commit --amend                      # Opens editor for message
git commit --amend -m "Fix bug in authentication module"    # Change message
git commit --amend --no-edit            # Keep message, just add changes
```

**Result:**
```
Before:  abc123 (Fix bug in autentication module) - BROKEN
After:   def456 (Fix bug in authentication module) - FIXED
         # SHA changed, old commit discarded
```

### Multiple Recent Commits

**Interactive Rebase**
```bash
# Fix one of the last 3 commits
git rebase -i HEAD~3

# Editor opens:
pick abc123 Initial implementation
pick def456 Fix missing validation    # This commit has bug
pick ghi789 Add tests

# Change 'pick' to 'edit' for the broken commit
edit abc123 Initial implementation
pick def456 Fix missing validation
pick ghi789 Add tests

# Git stops at that commit
# Fix the code
git add .
git commit --amend -m "Fixed message if needed"
git rebase --continue               # Move to next commit

# All set!
```

### Reordering or Squashing Commits

```bash
git rebase -i HEAD~5

# Reorder commits:
pick abc123 First
pick def456 Third              # Move up
pick ghi789 Second

# Squash commits:
pick abc123 First
squash def456 Include this too  # Combines with abc123
squash ghi789 And this         # Combines with result

# Drop commits:
pick abc123 Keep this
drop def456 Discard this
```

### Old/Published Commits (Use Revert)

**If commit already pushed, don't rewrite it!**

```bash
# Create new commit that undoes the broken one
git revert <broken-commit-sha>      # Creates inverse commit

# Or specific files
git revert --no-commit <sha>
git reset HEAD src/auth.js          # Unstage one file
git commit -m "Revert broken auth changes"
```

**Example:**
```bash
# Commit abc123 broke production login
git revert abc123               # Creates commit that undoes it

# Git log shows:
# def456 Revert "Fix login"
# abc123 Fix login             # Original, now undone
# ghi789 Add feature
```

### Complex Repair: Cherry-Pick

```bash
# Extract good changes from broken commit
# Create new branch with clean history
git checkout -b fix/clean-history

# Cherry-pick good commits up to broken one
git cherry-pick abc123
git cherry-pick ghi789          # Skip def456 (broken)

# Now manually make the fix
# ... code edits ...
git add .
git commit -m "Proper fix for the issue"

# Result: clean history without broken commit
```

### Abort and Start Over

```bash
# If rebase/revert goes wrong
git rebase --abort
git revert --abort

# Return to original state
# Then try different approach
```

---

## 21. Git Architecture

[See question #12 for comprehensive Git architecture explanation]

---

## 22. How to Check Branch Name

**Different ways to identify the current branch**

```bash
# Simple and most common
git branch --show-current

# Using rev-parse
git rev-parse --abbrev-ref HEAD

# From git status
git status                              # Shows "On branch main"

# Using symbolic-ref
git symbolic-ref --short HEAD

# Manual check
cat .git/HEAD                           # Shows: ref: refs/heads/main

# In shell scripts/aliases
BRANCH=$(git rev-parse --abbrev-ref HEAD)
echo "Current branch: $BRANCH"
```

### Using in Scripts/Aliases

```bash
# Add to ~/.zshrc or ~/.bashrc
alias gbranch='git rev-parse --abbrev-ref HEAD'

# Use in script
current_branch=$(git rev-parse --abbrev-ref HEAD)
git push origin $current_branch
```

### Interactive Branch Selection

```bash
# See all branches with * marking current
git branch

# List with more info
git branch -v                           # Shows last commit
git branch -v --contains HEAD           # Shows branches with current commit
```

---

## 23. Have You Come Across Any Merge Conflict

**Interview Answer Template**

"Yes, I've dealt with merge conflicts several times. Let me describe a specific example:

**Situation:**
- My teammate and I were working on different features
- Both modified the same configuration file
- When I merged their PR into main, Git couldn't auto-merge

**Conflict Details:**
- In `config/database.js`, we both changed the connection timeout setting
- They set it to 5000ms, I set it to 3000ms
- They also added error retry logic I hadn't seen

**How I Resolved It:**
1. Used `git status` to find conflicted files
2. Opened the file and saw conflict markers
3. Reviewed both versions in the file
4. Made a judgment call: their timeout was more appropriate for production, so I kept their value
5. But I also wanted their error retry logic, so I combined both changes
6. Tested the application locally to ensure it still worked
7. Ran our test suite to catch any integration issues
8. Committed the resolved changes with a message explaining the resolution

**What I Learned:**
- Communication is key — we should have discussed the timeout setting beforehand
- Smaller PRs lead to fewer conflicts
- Always test after resolving conflicts
- Use `git diff` to understand both sides of the conflict before deciding"

**Variations of Answer:**
- Conflicts in JSON configuration files
- Conflicts in migration files (database schema)
- Conflicts in frequently-edited files (package.json, dependencies)
- Conflicts from concurrent feature work

---

## 24. Creating Branch and Merging and Push, Pulling How You Do It

**Complete workflow from branch creation to merge**

### Step-by-Step Workflow

**1. Create Feature Branch**
```bash
# Update main first
git checkout main
git pull origin main

# Create feature branch
git checkout -b feature/user-profile-page

# Or modern syntax
git switch -c feature/user-profile-page
```

**2. Development Work**
```bash
# Make changes
# ... edit files: ProfilePage.js, ProfileStyles.css ...

# Stage and commit frequently
git add src/components/ProfilePage.js
git commit -m "Create profile page component"

git add src/styles/ProfileStyles.css
git commit -m "Add styling for profile page"

git add src/services/profileService.js
git commit -m "Add API service for profile data"

# Push to remote
git push -u origin feature/user-profile-page
# -u sets up tracking so future pushes are simpler
```

**3. Open Pull Request**
```bash
# Go to GitHub and create PR
# Or via command line
gh pr create --title "Add user profile page" \
    --body "Implements user profile with edit functionality"

# Request reviewers
# Link to related issues
```

**4. Code Review**
```bash
# Teammates review, maybe request changes

# If feedback: make fixes locally
# ... edit files based on feedback ...
git add .
git commit -m "Address review feedback: improve error handling"
git push origin feature/user-profile-page

# Updated PR automatically
```

**5. Approval and Merge**
```bash
# After approval, merge on GitHub web UI
# Or command line:

# Update local before merge
git fetch origin
git merge origin/feature/user-profile-page

# Or rebase for linear history
git rebase origin/feature/user-profile-page

# Merge to main
git checkout main
git pull origin main
git merge --no-ff feature/user-profile-page

# Or squash commits
git merge --squash feature/user-profile-page
git commit -m "Add user profile page feature"

# Push merge
git push origin main
```

**6. Clean Up**
```bash
# Delete local branch
git branch -d feature/user-profile-page

# Delete remote branch
git push origin --delete feature/user-profile-page

# Or prune all deleted branches
git fetch -p
```

**7. Update Others**
```bash
# Teammates pull your changes
git checkout main
git pull origin main

# Their feature branch now behind
git checkout feature/their-feature
git rebase origin/main              # Update with your changes
git push origin feature/their-feature
```

### Common Issues During This Workflow

**Conflict During Merge**
```bash
git merge origin/feature/user-profile-page
# CONFLICT! Both modified src/components/app.js

# Resolve (see question #4 for details)
# Then:
git add src/components/app.js
git commit -m "Resolve merge conflict"
```

**Need to Update Branch While Reviewing**
```bash
# Main moved forward with other PRs
git fetch origin
git rebase origin/main
git push origin feature/user-profile-page --force-with-lease
# Force push only if necessary, use --force-with-lease to prevent accidents
```

**Accidental Commit on Main**
```bash
# Oops, committed directly to main
git reset HEAD~1                    # Undo commit, keep changes
git checkout -b feature/oops
git commit -m "Proper feature commit"
git push origin feature/oops

# Create PR instead
```

---

## 25. Git Fetch & Git Pull

[See question #6 for comprehensive fetch vs pull explanation]

---

## 26. Git Merge & Git Rebase

[See question #15 for comprehensive merge vs rebase explanation]

---

## 27. Git diff-tree?

**What is `git diff-tree` and how to use it?**

`git diff-tree` is a low-level Git command (plumbing) that compares tree objects directly.

### What It Does
- Compares the tree object of one commit with another (or its parent)
- Shows which files changed, what type of change (add, modify, delete)
- Optionally shows the actual diff (patch)
- Useful for scripting and automation

### Syntax
```bash
git diff-tree [options] <commit>
git diff-tree [options] <commit1> <commit2>
```

### Common Usage

**Show Changes in Specific Commit**
```bash
# Compare HEAD with its parent
git diff-tree HEAD

# Output shows files changed in latest commit
:100644 100644 abc123 def456 M src/app.js
:000000 100644 000000 ghi789 A src/new-file.js
:100644 000000 jkl012 000000 D src/removed-file.js

# Fields: old-mode new-mode old-sha new-sha status path
```

**Show Files Changed Only**
```bash
git diff-tree --name-only HEAD
# Output:
# src/app.js
# src/new-file.js
# src/removed-file.js
```

**Show Files with Status**
```bash
git diff-tree --name-status HEAD
# Output:
# M  src/app.js            (Modified)
# A  src/new-file.js       (Added)
# D  src/removed-file.js   (Deleted)
# R src/old-name.js src/new-name.js  (Renamed)
```

**Show Full Patch**
```bash
git diff-tree -p HEAD
# Shows full diff like `git show`
```

**Compare Two Commits**
```bash
git diff-tree abc123 def456
# Shows what changed from abc123 to def456
```

**Merge Commits (Multiple Parents)**
```bash
# For merge commits, compare against each parent
git diff-tree -m <merge-commit>
# Shows what changed compared to first parent
# And what changed compared to second parent
```

### Real-World Usage

**In CI/CD Scripts:**
```bash
#!/bin/bash
# Run tests only for changed files
changed_files=$(git diff-tree --name-only HEAD~1 HEAD)
for file in $changed_files; do
    echo "Testing $file"
    pytest "tests/test_${file%.*}.py"
done
```

**Git Hooks:**
```bash
# .git/hooks/pre-commit
#!/bin/bash
# Prevent commits with debug code
git diff-tree --cached HEAD | grep -i "console.log"
if [ $? -eq 0 ]; then
    echo "Remove debug statements"
    exit 1
fi
```

**Automation Tools:**
```bash
# Generate changelog from commits
git log --all | while read commit; do
    git diff-tree --name-status "$commit" | \
        awk '{print "- " $2 ": " $1}'
done
```

---

## 28. How Do You Handle Merge Conflict?

[See question #4 for comprehensive merge conflict handling]

### Quick Reference
```bash
# Before merge, prepare
git fetch origin
git merge origin/feature

# If conflict
git status                              # Identify files
# Edit files, resolve markers
git add conflicted-file.js
git commit -m "Resolve merge conflict"

# If rebase
git rebase origin/main
# ... resolve conflicts ...
git add .
git rebase --continue
```

---

## 29. How You Check Diff Between Previous & Current Commit?

**Compare commits to see what changed**

### View Changes Between Commits

**Last Commit Only**
```bash
git show HEAD                           # Show last commit with diff
git show --stat HEAD                    # Summary of changes
```

**Between Two Commits**
```bash
git diff HEAD~1 HEAD                    # Last 2 commits
git diff abc123 def456                  # Specific commits by SHA
git diff v1.0.0 v1.0.1                 # Between tags
```

**Specific File**
```bash
git diff HEAD~1 HEAD src/app.js         # File changes between commits
git show HEAD:src/app.js                # View file as it was in HEAD
git show HEAD~1:src/app.js              # View file from previous commit
```

**Summary Only**
```bash
git diff --stat HEAD~1 HEAD             # File statistics
git diff --name-only HEAD~1 HEAD        # Just filenames
git diff --name-status HEAD~1 HEAD      # Filenames with status
```

### Useful Diff Options

```bash
git diff --word-diff HEAD~1 HEAD        # Show changes within lines
git diff --color-words HEAD~1 HEAD      # Colored word diff
git diff -w HEAD~1 HEAD                 # Ignore whitespace
git diff -U5 HEAD~1 HEAD                # 5 lines of context
```

### Viewing Diff by Line

```bash
# Which commit changed this line?
git blame src/app.js                    # Show who changed each line

# Detailed change for specific line
git log -p -S "searchTerm"              # Commits containing text

# All commits affecting file
git log --follow --oneline src/app.js   # History even if renamed
```

### Comparing Branches

```bash
git diff main feature                   # Feature changes vs main
git log main..feature                   # Commits in feature not in main
git diff main...feature                 # Changes since they diverged
```

---

## 30. What is Git Rebase? Why Can't You Use Rebase Instead of Merge?

[See question #15 for comprehensive rebase explanation]

### When NOT to Use Rebase

**Never rebase public/shared commits!**

```bash
# BAD: Rebase after pushing
git push origin feature
git rebase origin/main             # Changes history!
git push origin --force             # Breaks teammates' branches
```

**Why:**
- Other developers have the old commits
- Their branches depend on old SHAs
- You "disappear" commits they might have
- Extremely confusing and causes conflicts

**Solution:**
```bash
# Use merge instead for shared branches
git merge origin/main

# OK to rebase on personal/local work before pushing
git rebase origin/main
git push -u origin feature          # Never pushed before, safe
```

---

## 31. Git Fetch & Pull

[See question #6 for comprehensive explanation]

---

## 32. What is README File?

**Explain the README file and its importance**

A `README` is the first file developers read when encountering your project. It's typically in Markdown format (`README.md`).

### Purpose of README

1. **Project Description:** What does this project do?
2. **Quick Start:** How to get running in 5 minutes
3. **Installation:** Step-by-step setup
4. **Usage:** How to use the project
5. **Configuration:** Environment variables, settings
6. **Contributing:** How to contribute code
7. **License:** Legal terms
8. **Authors/Credits:** Who built this

### Typical README Structure

```markdown
# Project Name

One-liner description

## Overview
2-3 paragraph explanation of what this does

## Quick Start
Get running in 5 minutes:
```bash
git clone ...
npm install
npm start
```

## Requirements
- Node.js 14+
- MongoDB 4.4+
- npm 6+

## Installation
Detailed step-by-step installation

## Usage
How to use the project:
```javascript
const { function } = require('package');
function();
```

## Configuration
Environment variables needed

## API Documentation
If applicable

## Testing
How to run tests

## Contributing
1. Fork
2. Create branch
3. Make changes
4. Submit PR

## License
MIT

## Authors
Names and links
```

### Why README Matters

1. **First Impression:** Determines if people will try your project
2. **Reduces Questions:** Answers common setup questions
3. **Professional:** Shows you care about documentation
4. **Onboarding:** New team members get oriented faster
5. **SEO:** GitHub search indexes README content
6. **Open Source:** Critical for adoption

### Good README Characteristics

- Clear and concise
- Includes code examples
- Has badge/status indicators
- Links to documentation
- Shows current project status
- Lists contributors
- Clear contribution process

---

## 33. Git Webhooks

**What are Git webhooks and how are they used?**

Git webhooks are automated triggers that notify external services when repository events occur.

### How Webhooks Work

```
Event occurs in Git repo
    ↓
Webhook triggers
    ↓
HTTP POST to configured URL
    ↓
External service receives notification
    ↓
Service performs action (CI, deploy, etc)
```

### Common Webhook Events

```bash
push              # Code pushed to repo
pull_request      # PR opened/updated/closed
issues            # Issue created/commented
release           # Release published
pull_request_review  # PR review submitted
```

### Setting Up Webhooks

**GitHub Example:**
1. Go to repo Settings → Webhooks
2. Click "Add webhook"
3. Enter Payload URL: `https://ci.example.com/github`
4. Select events to trigger on
5. Save

**GitLab Example:**
1. Project Settings → Integrations → Webhooks
2. Add webhook
3. Configure URL and events
4. Save

### Webhook Payload Example

```json
{
  "action": "opened",
  "pull_request": {
    "id": 1,
    "title": "Add feature",
    "body": "Description",
    "user": {"login": "username"},
    "head": {"ref": "feature/x", "sha": "abc123"},
    "base": {"ref": "main"}
  },
  "repository": {
    "name": "my-project",
    "full_name": "user/my-project"
  }
}
```

### Common Webhook Uses

**1. Continuous Integration (CI)**
```
push event → Trigger tests
            → Run linter
            → Build application
            → Report results
```

**2. Continuous Deployment**
```
push to main → Build → Test → Deploy to staging
                              → Deploy to prod
```

**3. Notifications**
```
PR opened → Send Slack message
PR merged → Post to #deployments channel
```

**4. Issue Management**
```
PR linked to issue → Update issue status
PR merged → Close related issues
```

**5. Documentation**
```
push → Update docs site
       Generate API docs
       Update changelog
```

### Receiving Webhooks (Server Side)

**Node.js Example:**
```javascript
const express = require('express');
const app = express();

app.post('/github-webhook', express.json(), (req, res) => {
    const event = req.headers['x-github-event'];
    const payload = req.body;
    
    if (event === 'push') {
        console.log(`Push to ${payload.repository.name}`);
        // Trigger CI/CD
        runTests(payload);
    }
    
    res.status(200).send('OK');
});

app.listen(3000);
```

### Webhook Security

```bash
# GitHub provides secret signing
# Verify signature in your code
const crypto = require('crypto');

const signature = req.headers['x-hub-signature'];
const secret = process.env.GITHUB_WEBHOOK_SECRET;

const hash = crypto.createHmac('sha1', secret)
    .update(JSON.stringify(req.body))
    .digest('hex');

if (`sha1=${hash}` !== signature) {
    return res.status(401).send('Unauthorized');
}
```

### Debugging Webhooks

**GitHub:**
- Settings → Webhooks → Recent Deliveries
- View request/response for each trigger
- Replay failed webhooks

**GitLab:**
- Project Settings → Integrations → Webhooks
- Click webhook to see recent events

---

## 34. Where Do You Fix Bug? Will You Create a New Branch and Later How You Manage with Next Release

**Bug fix branching strategy and release management**

### Bug Fix Workflow

**Identify Bug Location**
```bash
# Bug reported: "Login broken in production"
# Confirm it's in current version
# Check git log/tags for when it was introduced
git log --oneline | head -20
git tag -l              # See releases
```

**Create Bug Fix Branch**

**For Active Development:**
```bash
# Branch from develop (Gitflow)
git checkout develop
git pull origin develop
git checkout -b bugfix/login-authentication-issue

# Or branch from main (GitHub Flow)
git checkout main
git pull origin main
git checkout -b fix/login-authentication-issue
```

**For Production Hotfix:**
```bash
# Critical bug in production, need immediate fix
git checkout main
git pull origin main
git checkout -b hotfix/critical-login-bug

# Fix code
# ... make changes and test ...

# Commit with clear message
git commit -m "Hotfix: Fix login authentication bug\n\nIncorrect token validation was rejecting valid tokens"

git push origin hotfix/critical-login-bug
```

### Code Review & Testing

```bash
# Open PR immediately (even if quick fix)
gh pr create --title "Hotfix: Login authentication bug"

# Assign reviewers (for urgent, maybe skip one reviewer)
# Run tests - must pass all
# Deploy to staging first
# Test in staging environment
# Get approval from team lead

# After approval, merge
git checkout main
git merge --no-ff hotfix/critical-login-bug
```

### Managing Release

**If bug in current release, two approaches:**

**Approach 1: Merge to both main and develop (Gitflow)**
```bash
# After merging hotfix to main
git checkout main
git merge hotfix/critical-login-bug
git tag -a v1.2.1 -m "Release 1.2.1 - Security hotfix"

# Also merge to develop
git checkout develop
git merge hotfix/critical-login-bug

# Now both branches have the fix
```

**Approach 2: Cherry-pick to release branch**
```bash
# Hotfix on main
git checkout main
git merge --no-ff hotfix/critical-login-bug

# Also apply to active release branch
git checkout release/v1.2.x
git cherry-pick <hotfix-commit>

# Now both main and release/v1.2.x have fix
```

### Managing for Next Release

**If bug found but not urgent:**
```bash
# Create branch from develop
git checkout -b bugfix/payment-calculation

# Fix and commit
git add src/payment.js
git commit -m "Fix: Incorrect tax calculation\n\nTax was doubled in edge cases"

# Open PR for next sprint/release
# Gets reviewed with other features

# Merge to develop when ready for next release
git checkout develop
git merge --no-ff bugfix/payment-calculation
```

### Tracking Bug Fixes

```bash
# Link PR to issue
# Title: "Fixes #456: Login broken"
# Body: "Closes #456"
# GitHub auto-closes issue when PR merges

# Track which versions have fix
git log --grep="Fixes #456"             # Show commits related to issue
git tag --contains <commit>             # Show versions with this fix
```

### Release Management with Multiple Bugs

```bash
# Sprint has multiple bug fixes
# Schedule release for next week

# During sprint: bugfix/* branches merge to develop

# At release time:
git checkout -b release/v1.3.0
git checkout main
git merge release/v1.3.0
git tag v1.3.0

# Includes all bugs fixed in sprint
# Release notes document all fixes
```

### Emergency Production Bug

```bash
# Production down!
# Create hotfix
git checkout -b hotfix/emergency-fix

# Make minimal fix
git commit -m "Emergency: Fix database connection timeout"

# Fast track through review (maybe just lead dev)
# Deploy immediately

# Then follow up
# - Root cause analysis
# - Merge to main and develop
# - Tag release
# - Create ticket for better solution next sprint
```

---

## 35. Share Screen and Write

**Interview Tip: Live Coding Demonstration**

When asked to share screen, be ready to:

**Demonstrate:**
```bash
# Create feature branch
git checkout -b feature/demo

# Make changes
# ... create/edit file ...

# Stage and commit
git add .
git commit -m "Demo feature"

# Push
git push -u origin feature/demo

# Show various git commands
git log --oneline
git diff main feature/demo
git branch -a

# Simulate merge
git checkout main
git merge feature/demo
```

**Be Prepared For:**
- Creating branches
- Making commits with good messages
- Resolving conflicts (if asked)
- Squashing commits
- Rebasing
- Pushing/pulling
- Checking history

**Tips:**
- Type slowly and clearly
- Explain what you're doing
- Use meaningful commit messages
- Test commands before using (don't be unsure)
- Be comfortable with your editor
- Know your git aliases if using them

---

## 36. Git Commands

[See question #10 for comprehensive Git commands list]

Be ready to run and explain:
```bash
git status
git log --oneline
git diff
git checkout -b feature/x
git add .
git commit -m "message"
git push origin branch
git merge feature/x
```

---

## 37. How Many Repos You Have in GitHub

**Interview Answer Template:**

"I have several repositories in GitHub:

**Personal Projects:**
- 3-4 portfolio projects demonstrating my skills
- Personal learning projects (practice repos)
- Configuration and dotfiles repository

**Professional Projects:**
- Several repositories from my current/previous companies (public or private)
- Contributions to open-source projects

**Most Significant Repos:**
1. [Project Name] - A full-stack web application showing my ability to...
2. [Project Name] - Demonstrates my DevOps/infrastructure knowledge
3. [Project Name] - Showcases my leadership and code review skills

**GitHub Stats:**
- Contributing regularly (commits most days)
- Active in open-source (PRs to X projects)
- Followers: X (shows community recognition)"

---

## 38. Explain All Types of Branches in Your Project

**Describe your branching structure**

**Answer Template:**

"In our Gitflow-based project, we maintain the following branches:

**Long-Lived Branches:**
- `main` - Production-ready code, deployed to production
- `develop` - Integration branch, includes completed features for next release

**Feature Branches** (`feature/*`)
- Purpose: Developing new features
- Created from: `develop`
- Merged back to: `develop`
- Lifetime: Duration of feature development (usually 1-2 weeks)
- Example: `feature/user-authentication`, `feature/payment-integration`

**Release Branches** (`release/*`)
- Purpose: Prepare for production release
- Created from: `develop` when ready to release
- Testing and bug fixes happen here
- Merged to: `main` (for release) and back to `develop` (for fixes)
- Tagged with version: `v1.2.0`
- Example: `release/v1.2.0`

**Hotfix Branches** (`hotfix/*`)
- Purpose: Quick fixes for production bugs
- Created from: `main` directly
- Merged back to: `main` (and `develop`)
- Short lifetime (hours to days)
- Example: `hotfix/critical-security-bug`

**Chore/Maintenance Branches** (`chore/*`)
- Purpose: Dependencies updates, refactoring
- Created from: `develop`
- Example: `chore/update-dependencies`, `chore/remove-dead-code`

**Branch Naming Convention:**
- Descriptive: `feature/user-profile-page` (not `feature/xyz` or `feature/1`)
- Lowercase with hyphens: `feature/two-factor-auth` (not `Feature/TwoFactorAuth`)
- Issue reference: `feature/issue-456-dark-mode`

**Branch Lifecycle:**
1. Created from appropriate parent
2. Work and regular commits
3. Open PR with description
4. Code review
5. Merge (squash/no-ff based on policy)
6. Delete branch (automated cleanup)

**Branch Protection Rules:**
- `main`: Require 2 approvals, all checks pass, up-to-date with develop
- `develop`: Require 1 approval, all checks pass, no force pushes"

---

## 39. Explain PR Process

[See question #5 for comprehensive PR process explanation]

**Quick Summary:**
1. Create feature branch
2. Open PR with description
3. CI/CD checks run
4. Code review requested
5. Address feedback (if any)
6. Approval granted
7. Merge to main
8. Deploy to staging/production
9. Delete branch

---

## 40. How Many Reviewers Are There

**Answer Template:**

"In our team, our code review policy is:

**Standard Requirements:**
- Minimum 2 approvals required before merge
- At least 1 from the code owners (senior developers or team leads)
- Cannot be self-approved

**For Different Risk Levels:**
- Regular features: 2 reviewers
- Hotfixes: Can be approved by 1 team lead (faster for urgent issues)
- Infrastructure changes: 3+ approvals, including DevOps
- Security-related: Review by security team member mandatory

**Reviewer Assignment:**
- Primary: Engineer directly familiar with the code area
- Secondary: Another team member for fresh perspective
- Optional: QA for testing-heavy changes

**SLA for Reviews:**
- Standard PR: Response within 4 hours
- Hotfix: Response within 30 minutes
- Blocked by review: Comment in PR within 2 hours

**We use GitHub code owners file** to automate reviewer assignment:
```
src/auth/     @auth-team
src/payments/ @payments-team
src/ui/       @frontend-team
```

**Review Process:**
1. Submitter requests reviewers
2. Reviewers add comments
3. Submitter addresses feedback
4. Reviewers re-approve
5. Merge when all approvals obtained"

---

## 41. About Version Control Tool

[See question #18 for comprehensive version control tool explanation]

---

## 42. What is `git rev-parse`? What's the Use

**Understanding and using `git rev-parse`**

### What `git rev-parse` Does

`git rev-parse` parses Git references and expressions, converting them to commit SHAs or other useful information.

### Common Uses

**Get Commit SHA**
```bash
git rev-parse HEAD                      # SHA of current commit
git rev-parse main                      # SHA of main branch tip
git rev-parse feature/xyz               # SHA of specific branch
git rev-parse v1.2.0                    # SHA of tag

# Output: abc123def456789...
```

**Get Current Branch Name**
```bash
git rev-parse --abbrev-ref HEAD
# Output: main or feature/xyz
```

**Resolve Ambiguous References**
```bash
git rev-parse HEAD~2                    # Commit 2 before HEAD
git rev-parse HEAD~                     # Parent of HEAD
git rev-parse HEAD^                     # Also parent of HEAD
git rev-parse @{-1}                     # Previously checked out branch
```

**Verify Commit Exists**
```bash
git rev-parse abc123def456 > /dev/null 2>&1
if [ $? -eq 0 ]; then
    echo "Commit exists"
else
    echo "Commit not found"
fi
```

### Scripting with `git rev-parse`

**Get Repository Root**
```bash
git rev-parse --show-toplevel           # Absolute path to repo root

# Useful in scripts:
cd $(git rev-parse --show-toplevel)
```

**Get Git Directory Path**
```bash
git rev-parse --git-dir                 # Path to .git directory
```

**Check if Inside Repository**
```bash
git rev-parse --is-inside-work-tree
# Output: true or false
```

### Real-World Examples

**Shell Script: Get Current Commit**
```bash
#!/bin/bash
current_commit=$(git rev-parse HEAD)
current_branch=$(git rev-parse --abbrev-ref HEAD)
echo "Branch: $current_branch, Commit: $current_commit"
```

**CI/CD Pipeline: Create Build ID**
```bash
BUILD_ID=$(git rev-parse HEAD | cut -c1-7)
echo "Building version $BUILD_ID"
docker build -t myapp:$BUILD_ID .
```

**Git Hook: Prevent commits to main**
```bash
#!/bin/bash
# .git/hooks/pre-commit
current_branch=$(git rev-parse --abbrev-ref HEAD)
if [ "$current_branch" = "main" ]; then
    echo "Cannot commit directly to main"
    exit 1
fi
```

**Deployment Script: Get Previous Version**
```bash
#!/bin/bash
previous_tag=$(git rev-parse HEAD~1@{tags})
current_tag=$(git rev-parse HEAD@{tags})
echo "Deploying from $previous_tag to $current_tag"
```

### Comparison with Alternatives

```bash
# All get current commit SHA:
git rev-parse HEAD
git log -1 --format=%H
git show -s --format=%H HEAD
git diff-tree --no-commit-id -r HEAD | head -1

# git rev-parse is the lightest and fastest
```

---

## Summary

This comprehensive guide covers 42 Git interview questions with detailed explanations, real-world scenarios, and practical examples. Use this document to:

1. **Prepare for interviews:** Understand each topic deeply
2. **Learn Git better:** Real-world scenarios and workflows
3. **Reference guide:** Come back when you need to explain concepts
4. **Teaching tool:** Help teammates understand Git

Good luck with your interviews!
