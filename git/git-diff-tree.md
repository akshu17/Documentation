# git diff-tree

## Overview

`git diff-tree` is a low-level Git command (a "plumbing" command) that compares Git tree objects — typically a commit and its parent(s) — and prints the differences between them. It is commonly used in scripts and for commit-level inspection rather than interactive working-tree diffs.

## Syntax

```
git diff-tree [options] <commit> [<commit>...]
```

If you run it on `HEAD`, it compares the `HEAD` commit's tree with its parent(s).

## Common options

- `-p` : show the patch (full diff)
- `-r` : recurse into subtrees (descend into directories)
- `--name-only` : list changed file paths only
- `--name-status` : list changed paths with status letters (A = added, M = modified, D = deleted)
- `--no-commit-id` : suppress commit IDs in the output
- `-m` : for merges, produce a separate diff against each parent
- `--root` : include diff for the initial commit (no parent)

## Examples

- Show the patch introduced by `HEAD`:

```
git diff-tree -p HEAD
```

- List files changed by a specific commit (paths only):

```
git diff-tree --no-commit-id --name-only -r <commit>
```

- Show changed files and their statuses for a commit:

```
git diff-tree -r --name-status <commit>
```

## `git diff-tree` vs `git diff`

- `git diff` is the porcelain (user-facing) command used to compare the working tree, index, or commits interactively; it supports many higher-level workflows.
- `git diff-tree` works directly on tree objects (commits) and is intended for scripting and plumbing. It does not compare the working directory unless you explicitly compare commit trees.

## Notes and tips

- If you typed `git diff -tree` (with a space), that's not correct — use `git diff-tree` (no space).
- For most interactive needs, `git show <commit>` or `git diff <commit>^!` may be more convenient; `git diff-tree` is handy in scripts or when you need precise tree-level output.

## Quick reference (useful snippets)

- Show patch for most recent commit:

```
git diff-tree -p HEAD
```

- Files changed by commit (list):

```
git diff-tree --no-commit-id --name-only -r <commit>
```

---

Created to explain `git diff-tree` and common usages.
