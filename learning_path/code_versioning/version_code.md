# Git & GitHub: A Complete Guide and Best Practices

> A practical guide for developers who want to use version control effectively in collaborative projects.

---

## Table of Contents

1. [What is Git?](#what-is-git)
2. [What is GitHub?](#what-is-github)
3. [Git vs GitHub](#git-vs-github)
4. [Core Concepts](#core-concepts)
5. [Branch Naming Conventions](#branch-naming-conventions)
6. [Commit Best Practices](#commit-best-practices)
7. [Branching Strategies](#branching-strategies)
8. [Pull Requests & Code Reviews](#pull-requests--code-reviews)
9. [Repository Rules & Protections](#repository-rules--protections)
10. [.gitignore Best Practices](#gitignore-best-practices)
11. [Useful Git Commands Cheatsheet](#useful-git-commands-cheatsheet)

---

## What is Git?

**Git** is a free, open-source **distributed version control system** created by Linus Torvalds in 2005. It tracks changes in source code during software development, enabling multiple developers to collaborate on the same project without overwriting each other's work.

At its core, Git allows you to:

- **Record the full history** of every change made to a project
- **Revert** to any previous state of your code
- **Branch** to work on features or fixes in isolation
- **Merge** changes from different developers seamlessly
- **Collaborate** without a central server (distributed architecture)

Git stores data as **snapshots**, not differences. Each time you commit, Git saves a picture of all your files at that moment. This makes it extremely fast and reliable.

---

## What is GitHub?

**GitHub** is a cloud-based platform that hosts Git repositories and adds collaboration tools on top of them. Acquired by Microsoft in 2018, it is the world's largest code hosting platform with over 100 million developers.

GitHub provides:

- **Remote repository hosting** — your code is stored and accessible online
- **Pull Requests (PRs)** — propose, discuss, and review code changes
- **Issues** — track bugs, enhancements, and tasks
- **GitHub Actions** — CI/CD automation pipelines
- **Branch protection rules** — enforce quality gates before merging
- **GitHub Pages** — host static websites directly from a repo
- **Security features** — Dependabot alerts, secret scanning, code scanning

> Alternatives to GitHub include **GitLab**, **Bitbucket**, and **Gitea** (self-hosted), but the concepts in this guide apply to all of them.

---

## Git vs GitHub

| Feature | Git | GitHub |
|---|---|---|
| Type | CLI tool / software | Web platform / service |
| Works offline | ✅ Yes | ❌ No |
| Stores history | ✅ Locally | ✅ Remotely |
| Collaboration tools | ❌ No | ✅ Yes (PRs, Issues…) |
| Cost | Free | Free (with paid tiers) |
| Created by | Linus Torvalds | Tom Preston-Werner et al. |

**In short:** Git is the engine; GitHub is the garage where you park and share it.

---

## Core Concepts

Understanding these terms is essential before applying any best practice.

### Repository (Repo)
A directory tracked by Git. It contains all your project files and the complete history of changes (stored in a hidden `.git/` folder).

### Commit
A snapshot of your changes at a given point in time. Each commit has a unique SHA hash, an author, a timestamp, and a message.

### Branch
A lightweight, movable pointer to a specific commit. Branches let you develop features in isolation without affecting the main codebase.

### Merge
Integrating changes from one branch into another.

### Rebase
An alternative to merge — replays commits from one branch on top of another to produce a cleaner, linear history.

### Remote
A version of your repository hosted on a server (e.g., `origin` on GitHub).

### Pull / Push
- `git pull` — fetch and integrate remote changes into your local branch
- `git push` — send your local commits to the remote repository

### HEAD
A pointer to the current commit you are working from. Usually it points to the tip of your current branch.

---

## Branch Naming Conventions

A consistent branch naming convention makes it immediately clear **what** is being worked on and **why**.

### Recommended Format

```
<type>/<short-description>
```

Or with a ticket/issue number:

```
<type>/<ticket-id>-<short-description>
```

### Common Types

| Prefix | Purpose | Example |
|---|---|---|
| `feature/` | New feature or enhancement | `feature/user-authentication` |
| `fix/` | Bug fix | `fix/login-redirect-loop` |
| `hotfix/` | Urgent production fix | `hotfix/payment-crash` |
| `chore/` | Maintenance, tooling, dependencies | `chore/update-dependencies` |
| `refactor/` | Code restructuring without behavior change | `refactor/auth-service` |
| `docs/` | Documentation only | `docs/api-reference` |
| `test/` | Adding or fixing tests | `test/user-service-coverage` |
| `release/` | Release preparation | `release/v2.3.0` |

### Rules

- Use **lowercase** and **hyphens** (no underscores or spaces)
- Keep it **short but descriptive** — aim for under 50 characters
- Include the **ticket/issue ID** when applicable: `feature/GH-142-dark-mode`
- **Avoid generic names** like `fix/bug`, `feature/new`, or `my-branch`

---

## Commit Best Practices

A good commit message is a letter to your future self (and teammates). It should answer: **"Why was this change made?"**

### The Conventional Commits Standard

The [Conventional Commits](https://www.conventionalcommits.org/) specification is widely adopted. The format is:

```
<type>(<scope>): <short summary>

[optional body]

[optional footer(s)]
```

#### Types

| Type | When to use |
|---|---|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes |
| `style` | Formatting, missing semicolons (no logic change) |
| `refactor` | Code restructuring |
| `test` | Adding or updating tests |
| `chore` | Build process, dependency updates |
| `perf` | Performance improvements |
| `ci` | CI/CD configuration changes |
| `revert` | Reverts a previous commit |

#### Examples

```
feat(auth): add OAuth2 login with Google

fix(cart): prevent duplicate items on rapid clicks

docs(readme): update local setup instructions

chore(deps): bump lodash from 4.17.20 to 4.17.21

refactor(api): extract user validation into separate service

feat(payments)!: migrate to Stripe v3 API

BREAKING CHANGE: PaymentService.charge() now returns a Promise
```

### Golden Rules for Commits

1. **Commit early, commit often** — small, focused commits are easier to review and revert
2. **One logical change per commit** — don't mix a bug fix with a feature in the same commit
3. **Write in the imperative mood** — "Add feature" not "Added feature" or "Adding feature"
4. **Keep the summary line under 72 characters**
5. **Use the body to explain the *why*, not the *what*** — the diff already shows what changed
6. **Never commit broken code** to a shared branch
7. **Never commit sensitive data** (passwords, API keys, tokens)

### What NOT to do

```bash
# ❌ Bad commit messages
git commit -m "fix"
git commit -m "WIP"
git commit -m "asdfgh"
git commit -m "changes"
git commit -m "stuff"
git commit -m "it works now"

# ✅ Good commit messages
git commit -m "fix(auth): resolve token expiry not being handled in refresh flow"
git commit -m "feat(dashboard): add real-time sales chart using WebSockets"
```

---

## Branching Strategies

Choose a branching strategy that fits your team's release cadence.

### Git Flow

Best for projects with **scheduled releases** and versioning.

```
main        ←── stable production code
develop     ←── integration branch for features
feature/*   ←── individual features branched from develop
release/*   ←── release preparation branched from develop
hotfix/*    ←── urgent fixes branched from main
```

**Workflow:**
1. Branch `feature/X` from `develop`
2. Merge back into `develop` via PR
3. When ready to release, branch `release/vX.Y.Z` from `develop`
4. Merge release into both `main` and `develop`
5. Tag the merge commit on `main`

### GitHub Flow

Best for teams doing **continuous deployment**.

```
main        ←── always deployable
feature/*   ←── any work branched from main
```

**Workflow:**
1. Branch from `main`
2. Commit your changes
3. Open a Pull Request
4. Review, CI passes → merge to `main`
5. Deploy immediately

### Trunk-Based Development

Best for **high-velocity teams** with strong CI/CD and feature flags.

```
main        ←── everyone merges here frequently (daily)
feature/*   ←── very short-lived branches (hours, not days)
```

Short-lived branches reduce merge conflicts to a minimum. Feature flags control what users see.

---

## Pull Requests & Code Reviews

Pull Requests (PRs) are the heart of collaborative development. They are the gate between a branch and a shared branch.

### A Good Pull Request

- Has a **clear, descriptive title** following conventional commit format
- Contains a **description** that explains: what changed, why, and how to test it
- Is **small and focused** — ideally under 400 lines of diff
- References the related **issue or ticket**: `Closes #142`
- Includes **screenshots or recordings** for UI changes
- Has **passing CI checks** before requesting review
- Has been **self-reviewed** by the author before requesting review

### PR Description Template

```markdown
## Summary
<!-- What does this PR do? -->

## Motivation
<!-- Why is this change needed? -->

## Changes
- Added X
- Refactored Y
- Removed Z

## How to Test
1. Step one
2. Step two

## Screenshots (if applicable)

## Related Issues
Closes #
```

### Code Review Best Practices

**As a reviewer:**
- Review the code, not the person — be kind and constructive
- Ask questions rather than making demands: "Could this be simplified with X?" vs "Do it this way."
- Approve when satisfied — don't leave PRs hanging
- Distinguish between blocking comments and nit-picks: prefix with `nit:` for optional suggestions
- Review for correctness, readability, security, and performance

**As an author:**
- Respond to every comment
- Don't take feedback personally
- If you disagree, explain your reasoning calmly
- Mark resolved threads once addressed

---

## Repository Rules & Protections

Protect your important branches from accidental or unauthorized changes.

### Branch Protection Rules (GitHub)

Apply these rules to `main` (and `develop` if using Git Flow):

- **Require pull request reviews before merging** — at least 1 approving review
- **Require status checks to pass** — CI must be green
- **Require branches to be up to date** — prevent merging stale branches
- **Restrict who can push** — only allow merges via PR
- **Require signed commits** — for extra security and traceability
- **Disable force pushes** — never allow `git push --force` to shared branches
- **Require linear history** — enforce rebasing over merge commits for a cleaner log

### Required CI Checks

Set up automated checks that must pass before any PR can be merged:

```
✅ Build passes
✅ Unit tests pass
✅ Integration tests pass
✅ Linting / code style (ESLint, Prettier, Pylint…)
✅ Type checking (TypeScript, mypy…)
✅ Code coverage threshold met
✅ Security scan (Dependabot, Snyk…)
```

### Semantic Versioning & Tags

Use **Semantic Versioning** (`MAJOR.MINOR.PATCH`) for releases:

```bash
git tag -a v1.4.2 -m "Release v1.4.2 - fix payment timeout"
git push origin v1.4.2
```

- **MAJOR** — breaking changes
- **MINOR** — new backward-compatible features
- **PATCH** — backward-compatible bug fixes

---

## .gitignore Best Practices

Never track files that shouldn't be in version control.

### What to Always Ignore

```gitignore
# Dependencies
node_modules/
vendor/
.venv/

# Build outputs
dist/
build/
*.egg-info/

# Environment & secrets
.env
.env.local
.env.production
*.pem
*.key

# IDE & OS files
.vscode/
.idea/
.DS_Store
Thumbs.db

# Logs & temp files
*.log
tmp/
.cache/
```

### Tips

- Use [gitignore.io](https://www.toptal.com/developers/gitignore) to generate templates for your stack
- Add a global `.gitignore` for your machine: `git config --global core.excludesfile ~/.gitignore_global`
- If you accidentally committed something sensitive, use `git filter-branch` or [BFG Repo Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) — and **rotate the exposed credentials immediately**

---

## Useful Git Commands Cheatsheet

### Setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.editor "code --wait"   # Use VS Code as editor
```

### Daily Workflow

```bash
git status                         # Check current state
git diff                           # Show unstaged changes
git add .                          # Stage all changes
git add -p                         # Interactively stage hunks
git commit -m "feat: add X"        # Commit with message
git push origin feature/my-branch  # Push to remote
git pull --rebase origin main      # Pull with rebase
```

### Branching

```bash
git branch                         # List local branches
git switch -c feature/my-feature   # Create and switch to new branch
git switch main                    # Switch branch
git branch -d feature/done         # Delete local branch
git push origin --delete feature/done  # Delete remote branch
```

### Merging & Rebasing

```bash
git merge feature/my-feature       # Merge branch into current
git rebase main                    # Rebase current branch onto main
git rebase -i HEAD~3               # Interactive rebase (last 3 commits)
```

### Undoing Things

```bash
git restore file.txt               # Discard unstaged changes
git restore --staged file.txt      # Unstage a file
git commit --amend                 # Amend the last commit
git revert <sha>                   # Create a revert commit (safe)
git reset --hard HEAD~1            # ⚠️ Discard last commit (destructive)
```

### Inspecting History

```bash
git log --oneline --graph --all    # Visual branch history
git log -p                         # Show commits with diffs
git blame file.txt                 # Who changed each line?
git show <sha>                     # Show a specific commit
git bisect start                   # Binary search for a bug
```

### Stashing

```bash
git stash                          # Save work in progress
git stash pop                      # Restore latest stash
git stash list                     # List all stashes
git stash drop stash@{0}           # Delete a stash
```

---

## Summary

Adopting good Git practices is an investment that pays off immediately. Here's a quick recap:

| Practice | Rule |
|---|---|
| **Branches** | Use `type/description` format, lowercase, hyphens |
| **Commits** | Small, focused, imperative mood, Conventional Commits |
| **PRs** | Small, described, linked to issue, self-reviewed first |
| **Reviews** | Kind, constructive, timely |
| **Protection** | Lock `main`, require CI, no force pushes |
| **Secrets** | Never commit them — use `.env` + `.gitignore` |
| **Tags** | Use Semantic Versioning for releases |

> Good version control habits are not just about tools — they are about **communication and respect** for your teammates, present and future.