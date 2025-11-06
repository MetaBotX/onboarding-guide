# Branch Management

Proper branch management keeps your repository clean, organized, and easy to navigate. This guide covers when and how to delete branches, keep them updated, and maintain good branch hygiene.

## When to Delete Branches

### ✅ After Successful Merge

Once a PR is merged, the branch has served its purpose and should be deleted:

```bash
# After PR is merged to develop/main
# Delete both local and remote branches
```

### ✅ After PR is Closed (Not Merged)

If a PR is closed without merging (abandoned, superseded, etc.), delete the branch:

```bash
# Branch is no longer needed
# Delete to avoid confusion
```

### ✅ Stale Feature Branches

Branches that haven't been updated in a long time (e.g., 3+ months) should be reviewed and likely deleted:

```bash
# Check for stale branches
git branch -a

# Review if branch is still needed
# If not, delete it
```

### ✅ Testing/Experimental Branches

Temporary branches created for testing or experiments:

```bash
# Experimental branches
feature/test-new-approach
test/performance-improvements
```

### ❌ Don't Delete

- Active branches with ongoing work
- Release branches that are currently in use
- Branches that contain important historical context
- `main`, `develop`, or other permanent branches

## How to Delete Branches

### Delete Local Branch

#### Safe Delete (Recommended)
```bash
# Delete branch only if it's been merged
git branch -d feature/your-feature-name

# If branch is merged, it will delete successfully
# If not merged, Git will warn you
```

#### Force Delete (Use with Caution)
```bash
# Force delete even if not merged
git branch -D feature/your-feature-name

# ⚠️ Warning: This deletes even unmerged changes!
# Only use if you're absolutely sure
```

### Delete Remote Branch

```bash
# Delete remote branch
git push origin --delete feature/your-feature-name

# Or using the shorter syntax
git push origin :feature/your-feature-name
```

### Delete Both Local and Remote

```bash
# 1. Delete remote branch
git push origin --delete feature/your-feature-name

# 2. Delete local branch
git branch -d feature/your-feature-name

# Or in one go (if you're sure it's merged)
git push origin --delete feature/your-feature-name && git branch -d feature/your-feature-name
```

### Using GitHub UI

Branch deletion through GitHub UI:

**GitHub:**
1. Go to repository → Branches
2. Find the branch
3. Click delete icon
4. Confirm deletion

## Bulk Cleanup Commands

### List All Branches

```bash
# List local branches
git branch

# List remote branches
git branch -r

# List all branches (local + remote)
git branch -a
```

### Delete Multiple Merged Branches

```bash
# Delete all local branches that have been merged into develop
git branch --merged develop | grep -v "\*\|develop\|main" | xargs -n 1 git branch -d

# More careful version (shows what will be deleted first)
git branch --merged develop | grep -v "\*\|develop\|main"

# Then delete if you're happy with the list
git branch --merged develop | grep -v "\*\|develop\|main" | xargs git branch -d
```

### Clean Up Remote Tracking Branches

```bash
# Remove remote tracking branches for deleted remote branches
git remote prune origin

# Or fetch with prune
git fetch --prune
```

### Delete All Local Branches Except Current

```bash
# ⚠️ Use with extreme caution!
git branch | grep -v "\*\|main\|develop" | xargs git branch -D
```

## Keeping Branches Updated

### Rebasing on Develop/Main

**Rebase (Recommended for cleaner history):**
```bash
# 1. Make sure you're on your feature branch
git checkout feature/your-feature-name

# 2. Fetch latest changes
git fetch origin

# 3. Rebase on develop
git rebase origin/develop

# 4. If conflicts occur, resolve them
# Edit conflicted files, then:
git add .
git rebase --continue

# 5. Force push (if you've rebased)
git push --force-with-lease origin feature/your-feature-name
```

**Merge (Alternative):**
```bash
# 1. Make sure you're on your feature branch
git checkout feature/your-feature-name

# 2. Merge develop into your branch
git merge origin/develop

# 3. Resolve conflicts if any
# Edit conflicted files, then:
git add .
git commit -m "chore: merge develop into feature branch"

# 4. Push changes
git push origin feature/your-feature-name
```

### Merging vs Rebasing

**Use Rebase when:**
- You want a linear, clean history
- Your branch is not shared with others
- You haven't pushed yet (or can force push)

**Use Merge when:**
- Branch is shared with others
- You want to preserve exact branch history
- You're not comfortable with rebase

### Resolving Conflicts

When updating your branch, you may encounter conflicts:

```bash
# 1. Rebase/merge triggers conflict
git rebase origin/develop
# Conflict detected in file.js

# 2. Open file and resolve conflicts
# Look for conflict markers:
<<<<<<< HEAD
your changes
=======
changes from develop
>>>>>>> origin/develop

# 3. Edit to resolve (keep what you need, remove markers)
# Your resolved code

# 4. Stage resolved files
git add file.js

# 5. Continue rebase/merge
git rebase --continue  # for rebase
# or
git commit  # for merge
```

### When to Update Your Branch

Update your branch:
- ✅ Before creating a PR
- ✅ Before pushing significant new changes
- ✅ When you see your branch is behind
- ✅ When requested by reviewers
- ✅ At least daily if working on active feature

## Branch Cleanup Automation

### GitHub Actions Auto-Delete

Create `.github/workflows/cleanup-branches.yml`:

```yaml
name: Auto Delete Merged Branches

on:
  pull_request:
    types: [closed]

jobs:
  delete-branch:
    runs-on: ubuntu-latest
    steps:
      - name: Delete branch
        if: github.event.pull_request.merged == true
        run: |
          git push origin --delete ${{ github.event.pull_request.head.ref }}
```

### Scheduled Cleanup Script

Example script to clean up stale branches:

```bash
#!/bin/bash
# cleanup-stale-branches.sh

# Find branches merged more than 30 days ago
git for-each-ref --format='%(refname:short) %(committerdate:relative)' refs/heads/ | \
  grep -E 'feature|bugfix|hotfix' | \
  while read branch date; do
    # Check if merged and old
    if git branch --merged develop | grep -q "$branch"; then
      echo "Deleting merged branch: $branch"
      git branch -d "$branch"
    fi
  done
```

### Manual Cleanup Procedures

**Weekly cleanup routine:**
1. List all branches: `git branch -a`
2. Identify merged branches: `git branch --merged develop`
3. Review each branch
4. Delete branches that are no longer needed
5. Clean up remote tracking: `git remote prune origin`

## Best Practices for Branch Hygiene

### Regular Cleanup Schedule

- **Daily**: Delete branches after PR merge
- **Weekly**: Review and clean up stale branches
- **Monthly**: Deep cleanup of old branches

### Naming Conventions to Avoid

Bad branch names that make cleanup difficult:
```
❌ test
❌ temp
❌ wip
❌ fix
❌ update
❌ my-branch
❌ johns-branch
```

### Branch Organization

**Organize by purpose:**
```
feature/user-authentication
feature/add-payment-gateway
bugfix/login-error
hotfix/security-patch
release/v1.2.0
```

**Use prefixes:**
- `feature/` - New features
- `bugfix/` or `fix/` - Bug fixes
- `hotfix/` - Critical production fixes
- `release/` - Release preparation
- `refactor/` - Code refactoring
- `docs/` - Documentation changes

### Tracking Active Branches

Keep track of:
- Which branches are actively being worked on
- Which branches are waiting for review
- Which branches are abandoned
- Which branches need to be merged

## Quick Reference

### Essential Commands

```bash
# List all branches
git branch -a

# Delete local branch (safe)
git branch -d branch-name

# Delete local branch (force)
git branch -D branch-name

# Delete remote branch
git push origin --delete branch-name

# Update branch with latest develop
git checkout branch-name
git rebase origin/develop

# Clean up remote tracking branches
git remote prune origin

# List merged branches
git branch --merged develop
```

### Cleanup Workflow

```bash
# 1. Update develop
git checkout develop
git pull origin develop

# 2. List merged branches
git branch --merged develop

# 3. Delete merged branches
git branch -d feature/old-feature-1
git branch -d feature/old-feature-2

# 4. Clean up remote references
git remote prune origin

# 5. Delete remote branches if needed
git push origin --delete feature/old-feature-1
```

## Common Issues

### Can't Delete Branch (Not Fully Merged)

```bash
# Git prevents deletion if branch has unmerged changes
error: The branch 'feature/xyz' is not fully merged.

# If you're sure you want to delete:
git branch -D feature/xyz
```

### Remote Branch Already Deleted

```bash
# Clean up stale remote tracking references
git remote prune origin
```

### Accidentally Deleted Branch

```bash
# Find the commit hash
git reflog

# Recreate branch from commit
git checkout -b feature/restored-branch <commit-hash>
```

## Tips

1. **Delete immediately after merge**: Don't let merged branches accumulate
2. **Regular cleanup**: Schedule time weekly/monthly for branch cleanup
3. **Use automation**: Set up automated cleanup where possible
4. **Communicate**: Let team know if you're deleting shared branches
5. **Double-check**: Always verify before force-deleting branches

---

**Next Steps**: Learn about [Commit Messages](commit-messages.md) to write clear, meaningful commits.

