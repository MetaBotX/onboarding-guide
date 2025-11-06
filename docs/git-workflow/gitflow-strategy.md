# Gitflow Branching Strategy

Gitflow is a branching model that helps organize development work and maintain a clean project history. This guide explains how MetaBotX uses Gitflow across our projects.

## Overview

Gitflow uses different branches for different purposes:
- **Main branches**: `main` and `develop`
- **Supporting branches**: `feature/*`, `release/*`, and `hotfix/*`

## Branch Types

### Main Branches

#### `main` (Production)
- Contains production-ready code
- Only updated through releases or hotfixes
- Protected branch - requires approval for merges
- Every commit should be tagged with a version number

#### `develop` (Integration Branch)
- Contains the latest development changes
- Branch for integration of features
- Used as the base branch for new features
- Should always be in a deployable state

### Supporting Branches

#### `feature/*` (Feature Branches)
- Created from `develop`
- Used for developing new features
- Naming: `feature/user-authentication`, `feature/add-payment-gateway`
- Merged back into `develop` when complete
- Never merged directly into `main`

#### `release/*` (Release Branches)
- Created from `develop` when preparing for a release
- Used for final bug fixes and preparation
- Naming: `release/1.2.0`, `release/v2.0.0`
- Merged into both `main` and `develop` when complete
- Tagged with version number after merge to `main`

#### `hotfix/*` (Hotfix Branches)
- Created from `main` for critical production fixes
- Used for urgent fixes that can't wait for the next release
- Naming: `hotfix/critical-security-patch`, `hotfix/database-connection-fix`
- Merged into both `main` and `develop`
- Tagged with version number after merge to `main`

## Branch Naming Conventions

### Good Branch Names
```
feature/user-login
feature/add-shopping-cart
release/v1.3.0
hotfix/payment-gateway-error
bugfix/incorrect-calculation
```

### Bad Branch Names
```
❌ fix
❌ new-feature
❌ update
❌ my-branch
❌ work-in-progress
❌ feature_user_login (use hyphens, not underscores)
```

**Guidelines:**
- Use lowercase letters
- Use hyphens to separate words
- Be descriptive but concise
- Include issue/ticket numbers if applicable: `feature/PROJ-123-user-authentication`

## Creating Feature Branches

### From Develop

```bash
# 1. Make sure you're on develop and it's up to date
git checkout develop
git pull origin develop

# 2. Create and switch to a new feature branch
git checkout -b feature/your-feature-name

# 3. Start working on your feature
# ... make changes ...

# 4. Commit your changes
git add .
git commit -m "feat: add user authentication"

# 5. Push to remote
git push origin feature/your-feature-name
```

## Workflow Diagram

```
main (production)
  │
  ├── hotfix/critical-bug ──┐
  │                         │
  │                         └──► main (tagged)
  │                                 │
  │                                 └──► develop
  │
  └── release/v1.2.0 ────────┐
                             │
                             └──► main (tagged)
                             │
                             └──► develop
                                    │
                                    ├── feature/user-login ──┐
                                    │                        │
                                    ├── feature/payments ────┤
                                    │                        │
                                    └── feature/dashboard ───┘
                                             │
                                             └──► develop (after merge)
```

## Merge Process

### Feature Branch → Develop

1. **Update your feature branch** with latest changes from develop:
   ```bash
   git checkout feature/your-feature-name
   git pull origin develop
   git rebase develop  # or git merge develop
   ```

2. **Resolve any conflicts** if they occur

3. **Push your updated branch**:
   ```bash
   git push origin feature/your-feature-name
   ```

4. **Create a Pull Request** from `feature/your-feature-name` to `develop`

5. **Get code review approval**

6. **Merge the PR** using the appropriate merge strategy (see [Merge Strategies](merge-strategies.md) for guidance)

7. **Delete the feature branch** (local and remote)

### Release Branch → Main and Develop

1. Create release branch from develop
2. Final bug fixes and version bump
3. Merge to main (tagged)
4. Merge back to develop

### Hotfix Branch → Main and Develop

1. Create hotfix branch from main
2. Fix the critical issue
3. Merge to main (tagged)
4. Merge back to develop

## Branch Protection Rules

Most MetaBotX repositories have branch protection rules for `main` and `develop`:

- **Require pull request reviews**: At least one approval required
- **Require status checks**: All CI/CD checks must pass
- **Require up-to-date branches**: Must be up to date with base branch
- **No direct pushes**: Must use pull requests
- **Include administrators**: Admins must also follow rules

## Common Scenarios

### Scenario 1: Starting a New Feature

```bash
# 1. Update local develop
git checkout develop
git pull origin develop

# 2. Create feature branch
git checkout -b feature/add-search-functionality

# 3. Work on your feature
# ... make changes and commits ...

# 4. Push to remote
git push -u origin feature/add-search-functionality
```

### Scenario 2: Updating Feature Branch with Latest Changes

```bash
# Option A: Merge (preserves history)
git checkout develop
git pull origin develop
git checkout feature/your-feature-name
git merge develop

# Option B: Rebase (cleaner history)
git checkout develop
git pull origin develop
git checkout feature/your-feature-name
git rebase develop

# If conflicts occur, resolve them and continue:
git rebase --continue

# Force push (only if you've rebased)
git push --force-with-lease origin feature/your-feature-name
```

### Scenario 3: Fixing a Critical Production Bug

```bash
# 1. Create hotfix from main
git checkout main
git pull origin main
git checkout -b hotfix/critical-payment-bug

# 2. Fix the bug
# ... make changes ...

# 3. Commit and push
git add .
git commit -m "fix: resolve payment gateway connection issue"
git push origin hotfix/critical-payment-bug

# 4. Create PRs to both main and develop
# 5. After merge, tag the version
git tag -a v1.2.1 -m "Hotfix: Payment gateway fix"
git push origin v1.2.1
```

### Scenario 4: Preparing a Release

```bash
# 1. Create release branch from develop
git checkout develop
git pull origin develop
git checkout -b release/v1.3.0

# 2. Update version numbers, changelog, etc.
# ... make changes ...

# 3. Final testing and bug fixes
# ... make changes ...

# 4. Merge to main
# Create PR: release/v1.3.0 → main

# 5. Tag the release
git checkout main
git tag -a v1.3.0 -m "Release version 1.3.0"
git push origin v1.3.0

# 6. Merge back to develop
# Create PR: release/v1.3.0 → develop
```

## Alternative Branching Strategies

### GitHub Flow (Simpler Alternative)

- `main` branch only
- Feature branches created from and merged back to `main`
- Deploy from `main`
- Good for: Continuous deployment, simpler projects

### Trunk-Based Development (Alternative)

- `main` branch
- Feature branches
- Environment branches: `staging`, `production`
- Good for: Projects with multiple deployment environments

## Quick Reference

### Essential Commands

```bash
# Switch to develop and update
git checkout develop && git pull origin develop

# Create feature branch
git checkout -b feature/your-feature-name

# Push new branch to remote
git push -u origin feature/your-feature-name

# Update branch with latest develop
git rebase develop  # or git merge develop

# List all branches
git branch -a

# Delete local branch
git branch -d feature/your-feature-name

# Delete remote branch
git push origin --delete feature/your-feature-name
```

## Best Practices

1. **Always start from develop**: Create feature branches from the latest `develop`
2. **Keep branches short-lived**: Feature branches should be merged within days/weeks, not months
3. **Keep develop deployable**: `develop` should always be in a working state
4. **Regular updates**: Update your feature branch regularly with changes from `develop`
5. **Clear naming**: Use descriptive, consistent branch names
6. **One feature per branch**: Keep branches focused on a single feature or fix
7. **Clean up**: Delete merged branches promptly

## Common Mistakes to Avoid

- ❌ Creating feature branches from `main`
- ❌ Merging directly to `main` without going through `develop`
- ❌ Working on the same feature in multiple branches
- ❌ Forgetting to merge hotfixes back to `develop`
- ❌ Leaving stale branches around for months
- ❌ Using vague branch names like "fix" or "update"

---

**Next Steps**: Read about [Pull Requests](pull-requests.md) and [Merge Strategies](merge-strategies.md) to learn how to merge your branches properly.

