# Development Workflow

This guide covers the daily workflow for developing features, making changes, and collaborating with your team. Follow these practices to ensure smooth development and collaboration.

## Daily Workflow

### Starting Your Day

```bash
# 1. Update your local develop branch
git checkout develop
git pull origin develop

# 2. Check what you're working on
git branch
# or check your PRs/issues

# 3. Switch to your feature branch (or create new one)
git checkout feature/your-feature-name
# or
git checkout -b feature/new-feature-name
```

### Creating a Feature Branch

```bash
# 1. Make sure develop is up to date
git checkout develop
git pull origin develop

# 2. Create and switch to new feature branch
git checkout -b feature/your-feature-name

# 3. Start working!
# Make your changes, write code, tests, etc.
```

### Making Changes

```bash
# 1. Make your code changes
# Edit files, write code, etc.

# 2. Stage your changes
git add .

# 3. Commit with a clear message
git commit -m "feat: add user authentication"

# 4. Push to remote
git push origin feature/your-feature-name
```

### Creating a Pull Request

1. **Push your branch** (if not already pushed)
2. **Go to GitHub** and create PR
3. **Write clear description** using PR template
4. **Request reviewers**
5. **Wait for review and feedback**

### Addressing Feedback

```bash
# 1. Make changes based on feedback
# Edit files, fix issues, etc.

# 2. Commit changes
git add .
git commit -m "fix: address review feedback"

# 3. Push updates
git push origin feature/your-feature-name

# 4. Respond to comments in PR
# Mark resolved, re-request review
```

### Merging and Cleanup

After PR is merged:

```bash
# 1. Switch back to develop
git checkout develop

# 2. Pull latest changes (including your merged PR)
git pull origin develop

# 3. Delete local feature branch
git branch -d feature/your-feature-name

# 4. Clean up remote tracking
git remote prune origin
```

## Git Workflow Commands

### Common Git Commands

```bash
# Status - see what's changed
git status

# Diff - see what changed
git diff                    # Unstaged changes
git diff --staged          # Staged changes
git diff HEAD               # All changes since last commit

# Log - see commit history
git log                     # Full history
git log --oneline          # Compact history
git log --graph --oneline  # Visual history

# Branch management
git branch                  # List local branches
git branch -a               # List all branches
git checkout -b new-branch  # Create and switch to new branch
git branch -d branch-name   # Delete branch

# Remote operations
git fetch origin            # Fetch latest from remote
git pull origin develop     # Fetch and merge
git push origin branch-name # Push branch to remote
```

### Stashing Changes

When you need to switch branches but have uncommitted changes:

```bash
# Stash current changes
git stash

# Stash with message
git stash save "WIP: working on auth feature"

# List stashes
git stash list

# Apply most recent stash
git stash apply

# Apply specific stash
git stash apply stash@{0}

# Apply and remove from stash
git stash pop

# Drop a stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

### Undoing Changes

```bash
# Unstage file (keep changes)
git reset HEAD file.js

# Unstage all files
git reset HEAD

# Discard changes to file (⚠️ destructive!)
git checkout -- file.js

# Discard all changes (⚠️ destructive!)
git checkout .

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes) (⚠️ destructive!)
git reset --hard HEAD~1

# Revert a commit (creates new commit)
git revert <commit-hash>
```

### Cherry-Picking

Copy a commit from another branch:

```bash
# Find commit hash
git log

# Cherry-pick commit
git cherry-pick <commit-hash>

# Cherry-pick multiple commits
git cherry-pick <hash1> <hash2> <hash3>

# Cherry-pick range
git cherry-pick <start-hash>..<end-hash>
```

## Working with Remote

### Fetch vs Pull

**Fetch** (safe, doesn't change your working directory):
```bash
# Fetch latest from remote (doesn't merge)
git fetch origin

# Fetch specific branch
git fetch origin develop

# See what changed
git log HEAD..origin/develop
```

**Pull** (fetches and merges):
```bash
# Fetch and merge
git pull origin develop

# Equivalent to:
git fetch origin develop
git merge origin/develop
```

### Tracking Branches

```bash
# Set upstream when pushing
git push -u origin feature/your-feature-name

# Set upstream for existing branch
git branch --set-upstream-to=origin/develop develop

# See tracking info
git branch -vv
```

### Upstream Configuration

```bash
# Add remote repository
git remote add upstream <repository-url>

# Fetch from upstream
git fetch upstream

# Merge upstream changes
git merge upstream/develop

# Update your fork
git push origin develop
```

## Collaboration

### Working on Shared Branches

When multiple people work on the same branch:

```bash
# 1. Before starting work, pull latest
git pull origin shared-branch-name

# 2. Make your changes
# ... work ...

# 3. Before pushing, pull again
git pull origin shared-branch-name

# 4. Resolve conflicts if any
# ... resolve conflicts ...

# 5. Push your changes
git push origin shared-branch-name
```

### Handling Merge Conflicts

```bash
# 1. Attempt merge/pull
git pull origin develop
# Conflict detected!

# 2. See conflicted files
git status

# 3. Open conflicted files
# Look for conflict markers:
<<<<<<< HEAD
your changes
=======
their changes
>>>>>>> origin/develop

# 4. Resolve conflicts
# Edit file, remove markers, keep desired code

# 5. Stage resolved files
git add file.js

# 6. Complete merge
git commit

# 7. Push
git push origin feature/your-feature-name
```

### Using Merge Tools

```bash
# Configure merge tool
git config --global merge.tool vimdiff
# or vscode, meld, etc.

# Use merge tool
git mergetool
```

### Coordinating with Team Members

- **Communicate**: Let team know what you're working on
- **Update regularly**: Keep your branch up to date
- **Resolve conflicts quickly**: Don't let conflicts sit
- **Share progress**: Update PRs, communicate blockers
- **Ask for help**: Don't struggle alone

## Best Practices

### Regular Commits

- **Commit often**: Small, logical commits
- **Commit before breaks**: Commit before leaving for the day
- **Commit working code**: Don't commit broken code
- **Commit atomic changes**: One logical change per commit

### Atomic Changes

Each commit should be a complete, logical unit:

```
✅ Good: One feature per commit
feat: add user login
feat: add user registration
feat: add password reset

❌ Bad: Multiple unrelated changes
feat: add login, registration, and password reset
```

### Meaningful Commit Messages

Follow [commit message guidelines](../git-workflow/commit-messages.md):
- Use conventional commits format
- Be clear and descriptive
- Explain why, not just what

### Keeping Branches Clean

- **Update regularly**: Sync with base branch frequently
- **Resolve conflicts early**: Don't let them accumulate
- **Delete merged branches**: Clean up after merge
- **One feature per branch**: Keep branches focused

## Workflow Examples

### Example 1: Starting a New Feature

```bash
# Morning routine
git checkout develop
git pull origin develop
git checkout -b feature/add-search

# Work on feature
# ... make changes ...
git add .
git commit -m "feat: add search functionality"
git push -u origin feature/add-search

# Create PR, get review, merge
# After merge:
git checkout develop
git pull origin develop
git branch -d feature/add-search
```

### Example 2: Updating Feature Branch

```bash
# Your feature branch is behind develop
git checkout feature/your-feature
git fetch origin
git rebase origin/develop

# If conflicts:
# Resolve conflicts
git add .
git rebase --continue

# Push updated branch
git push --force-with-lease origin feature/your-feature
```

### Example 3: Fixing a Bug in Your Feature

```bash
# While working on feature
git checkout feature/your-feature
# ... discover bug ...
# ... fix bug ...
git add .
git commit -m "fix: resolve search results bug"
git push origin feature/your-feature
```

### Example 4: Switching Between Tasks

```bash
# Working on feature A
git checkout feature/feature-a
# ... work ...

# Need to switch to urgent bug fix
git stash
git checkout develop
git checkout -b hotfix/critical-bug
# ... fix bug ...
git commit -m "fix: critical security issue"
git push origin hotfix/critical-bug

# Back to feature A
git checkout feature/feature-a
git stash pop
# ... continue work ...
```

## Quick Reference

### Daily Workflow Checklist

- [ ] Update develop branch
- [ ] Update feature branch if needed
- [ ] Make changes and commit
- [ ] Push changes regularly
- [ ] Update PR if exists
- [ ] Clean up merged branches

### Essential Commands

```bash
# Daily commands
git status
git add .
git commit -m "type: description"
git push origin branch-name
git pull origin develop

# Branch management
git checkout -b feature/new-feature
git branch -d feature/old-feature
git branch -a

# Conflict resolution
git pull origin develop
# Resolve conflicts
git add .
git commit
```

### Common Workflows

```bash
# Start new feature
git checkout develop && git pull && git checkout -b feature/new

# Update feature branch
git checkout feature/name && git rebase origin/develop

# Finish feature
git checkout develop && git pull && git branch -d feature/name
```

## Tips

1. **Pull before push**: Always pull latest before pushing
2. **Commit often**: Small, frequent commits are better
3. **Test before commit**: Don't commit broken code
4. **Use branches**: Never work directly on develop/main
5. **Keep branches updated**: Sync with base branch regularly
6. **Communicate**: Let team know what you're working on
7. **Ask for help**: Don't struggle with Git issues alone

---

**Next Steps**: Check the [Project Setup Checklist](project-setup.md) to ensure your environment is properly configured.

