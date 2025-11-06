# Example Git Workflow

This document walks through a complete example of working on a feature from start to finish, following best practices.

## Scenario

**Task:** Add user profile editing functionality
**Ticket:** #123
**Branch:** `feature/user-profile-editing`

## Step-by-Step Workflow

### Step 1: Update Local Repository

```bash
# Make sure you're on develop and it's up to date
git checkout develop
git pull origin develop

# Verify you're up to date
git status
```

**Output:**
```
On branch develop
Your branch is up to date with 'origin/develop'.
```

### Step 2: Create Feature Branch

```bash
# Create and switch to new feature branch
git checkout -b feature/user-profile-editing

# Verify branch was created
git branch
```

**Output:**
```
* feature/user-profile-editing
  develop
```

### Step 3: Make Initial Changes

```bash
# Make your code changes
# Edit files, add new files, etc.

# Check what changed
git status
```

**Output:**
```
On branch feature/user-profile-editing
Changes not staged for commit:
  modified:   src/services/userService.js
  modified:   src/api/userRoutes.js
Untracked files:
  src/components/UserProfileForm.js
  tests/userProfile.test.js
```

### Step 4: Stage and Commit Changes

```bash
# Stage all changes
git add .

# Commit with clear message
git commit -m "feat: add user profile editing functionality

- Add UserProfileForm component
- Update userService with editProfile method
- Add API endpoint for profile updates
- Add unit tests for profile editing

Closes #123"
```

**Output:**
```
[feature/user-profile-editing abc1234] feat: add user profile editing functionality
 4 files changed, 150 insertions(+), 12 deletions(-)
```

### Step 5: Push Branch to Remote

```bash
# Push branch to remote (first time)
git push -u origin feature/user-profile-editing
```

**Output:**
```
Enumerating objects: 15, done.
Counting objects: 100% (15/15), done.
Delta compression using up to 8 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (8/8), 1.2 KiB | 1.2 MiB/s, done.
Total 8 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), completed with 4 local objects.
To github.com:org/repo.git
 * [new branch]      feature/user-profile-editing -> feature/user-profile-editing
Branch 'feature/user-profile-editing' set up to track 'origin/feature/user-profile-editing'.
```

### Step 6: Continue Working (Additional Commits)

```bash
# Make more changes
# ... edit files ...

# Stage and commit
git add .
git commit -m "fix: add validation for profile email field"
```

### Step 7: Update Branch with Latest Develop

Before creating PR, update your branch:

```bash
# Fetch latest changes
git fetch origin

# Rebase on develop (or merge)
git rebase origin/develop
```

**If conflicts occur:**
```bash
# Resolve conflicts in files
# Edit conflicted files, remove conflict markers

# Stage resolved files
git add .

# Continue rebase
git rebase --continue
```

### Step 8: Push Updated Branch

```bash
# Push updated branch (force with lease after rebase)
git push --force-with-lease origin feature/user-profile-editing
```

### Step 9: Create Pull Request

Go to GitHub and create PR:
- Base: `develop`
- Compare: `feature/user-profile-editing`
- Write description using PR template
- Request reviewers
- Link issue #123

### Step 10: Address Review Feedback

```bash
# Reviewer suggests changes
# Make changes based on feedback

# Stage and commit
git add .
git commit -m "fix: address review feedback - add error handling"

# Push updates
git push origin feature/user-profile-editing

# Respond to comments in PR
# Re-request review when ready
```

### Step 11: PR Approved and Merged

After PR is approved and merged:

```bash
# Switch back to develop
git checkout develop

# Pull latest changes (including your merged PR)
git pull origin develop
```

**Output:**
```
Updating abc1234..def5678
Fast-forward
 src/services/userService.js      | 45 +++++++++++++++++
 src/api/userRoutes.js            | 12 ++++++
 src/components/UserProfileForm.js | 78 ++++++++++++++++++++++++++++
 tests/userProfile.test.js         | 56 ++++++++++++++++++++
 4 files changed, 191 insertions(+)
```

### Step 12: Clean Up Local Branch

```bash
# Delete local feature branch
git branch -d feature/user-profile-editing

# Clean up remote tracking
git remote prune origin
```

**Output:**
```
Deleted branch feature/user-profile-editing (was abc1234).
```

## Complete Example Session

Here's a complete example session:

```bash
# Morning: Start new feature
$ git checkout develop
Switched to branch 'develop'

$ git pull origin develop
Already up to date.

$ git checkout -b feature/user-profile-editing
Switched to a new branch 'feature/user-profile-editing'

# Work on feature
$ # ... make changes ...

$ git status
On branch feature/user-profile-editing
Changes not staged for commit:
  modified:   src/services/userService.js
  new file:   src/components/UserProfileForm.js

$ git add .
$ git commit -m "feat: add user profile editing functionality

- Add UserProfileForm component
- Update userService with editProfile method
- Add API endpoint for profile updates

Closes #123"

[feature/user-profile-editing abc1234] feat: add user profile editing functionality
 3 files changed, 120 insertions(+)

$ git push -u origin feature/user-profile-editing
Enumerating objects: 12, done.
...
To github.com:org/repo.git
 * [new branch]      feature/user-profile-editing -> feature/user-profile-editing

# Create PR on GitHub
# ... PR created, waiting for review ...

# Address feedback
$ # ... make changes based on review ...

$ git add .
$ git commit -m "fix: address review feedback - add error handling"
[feature/user-profile-editing def5678] fix: address review feedback - add error handling
 1 file changed, 15 insertions(+)

$ git push origin feature/user-profile-editing
...

# PR approved and merged
# Clean up
$ git checkout develop
Switched to branch 'develop'

$ git pull origin develop
Updating abc1234..def5678
Fast-forward
...
 4 files changed, 135 insertions(+)

$ git branch -d feature/user-profile-editing
Deleted branch feature/user-profile-editing (was abc1234).
```

## Common Workflow Variations

### Working with Multiple Commits

```bash
# Make several small commits
git commit -m "feat: add UserProfileForm component"
git commit -m "feat: add editProfile service method"
git commit -m "feat: add profile update API endpoint"
git commit -m "test: add unit tests for profile editing"

# Push all commits
git push origin feature/user-profile-editing
```

### Updating Branch Mid-Development

```bash
# While working on feature, develop has updates
git stash                    # Save current work
git checkout develop
git pull origin develop
git checkout feature/user-profile-editing
git rebase origin/develop   # Update feature branch
git stash pop               # Restore work
```

### Fixing a Bug in Your Feature

```bash
# Discover bug while working
# ... fix bug ...

git add .
git commit -m "fix: resolve profile validation error"
git push origin feature/user-profile-editing
```

### Squashing Commits Before PR

```bash
# Interactive rebase to squash commits
git rebase -i HEAD~4

# In editor, change "pick" to "squash" for commits to combine
# Save and write new commit message

# Force push (if already pushed)
git push --force-with-lease origin feature/user-profile-editing
```

## Tips

1. **Commit often**: Small, logical commits are better
2. **Update regularly**: Sync with develop frequently
3. **Test before commit**: Don't commit broken code
4. **Write clear messages**: Follow commit message guidelines
5. **Push regularly**: Don't let work accumulate locally
6. **Clean up**: Delete merged branches promptly

## Quick Reference

### Daily Workflow

```bash
# Start day
git checkout develop && git pull

# Work on feature
git checkout feature/your-feature
# ... make changes ...
git add . && git commit -m "type: description"
git push origin feature/your-feature

# End of day / After merge
git checkout develop && git pull
git branch -d feature/your-feature
```

### Essential Commands

```bash
# Branch management
git checkout -b feature/new-feature
git branch -d feature/old-feature

# Making changes
git add .
git commit -m "type: description"
git push origin feature/your-feature

# Updating branch
git fetch origin
git rebase origin/develop  # or git merge origin/develop

# Cleanup
git branch -d feature/merged-feature
git remote prune origin
```

