# Merge Strategies: Squash vs Rebase

At MetaBotX, we use specific merge strategies to maintain clean, readable project history. This guide explains when and how to use each merge strategy.

## Overview

When merging a Pull Request, GitHub provides three merge options:
1. **Squash and Merge** (Default)
2. **Rebase and Merge** (Rare, requires approval)
3. **Create a Merge Commit** (Not used at MetaBotX)

## MetaBotX Merge Strategy: Squash Merge (Default)

### When to Use Squash Merge

**Use Squash Merge for:**
- ✅ All feature branches
- ✅ Bug fix branches
- ✅ Documentation updates
- ✅ Refactoring branches
- ✅ Any PR that should appear as a single logical change

### How Squash Merge Works

Squash merge combines all commits from your feature branch into a single commit on the target branch.

**Before merge:**
```
develop:     A---B---C
                    \
feature:             D---E---F
```

**After squash merge:**
```
develop:     A---B---C---G (G contains changes from D, E, F)
```

### Benefits of Squash Merge

- **Clean history**: Each feature appears as one commit
- **Easy to understand**: Clear what each commit represents
- **Easy to revert**: Reverting a feature is a single commit
- **Professional appearance**: Clean, linear history

### Example

Your feature branch has these commits:
```
feat: add user authentication
fix: resolve login validation bug
test: add unit tests for auth
docs: update API documentation
```

After squash merge, it becomes one commit:
```
feat: add user authentication

- Implement OAuth2 login flow
- Add validation and error handling
- Add comprehensive unit tests
- Update API documentation

Closes #123
```

## Rebase Merge (Rare, Requires Approval)

### When to Use Rebase Merge

**Use Rebase Merge only when:**
- ⚠️ You need to preserve individual commit history
- ⚠️ Each commit represents a meaningful, standalone change
- ⚠️ You have explicit approval from your team lead
- ⚠️ The commits follow conventional commit format perfectly

**Rebase merge is rarely used at MetaBotX.** Default to squash merge unless there's a specific reason to preserve commit history.

### How Rebase Merge Works

Rebase merge replays each commit from your feature branch onto the target branch, preserving individual commits.

**Before merge:**
```
develop:     A---B---C
                    \
feature:             D---E---F
```

**After rebase merge:**
```
develop:     A---B---C---D'---E'---F'
```

### When NOT to Use Rebase Merge

- ❌ Feature branches with many small commits
- ❌ Branches with "WIP" or "fix typo" commits
- ❌ When commits don't follow conventional format
- ❌ Without team lead approval

## Create a Merge Commit (Not Used)

**MetaBotX does not use "Create a Merge Commit"** because it:
- Creates unnecessary merge commits
- Clutters the history
- Makes it harder to understand changes

## Decision Tree

```
Is this a feature branch?
├─ Yes → Use Squash Merge ✅
└─ No → Is this a hotfix?
    ├─ Yes → Use Squash Merge ✅
    └─ No → Do you need to preserve individual commits?
        ├─ Yes → Get team lead approval → Use Rebase Merge ⚠️
        └─ No → Use Squash Merge ✅
```

## MetaBotX Guidelines

### Default Behavior

**Always default to Squash Merge** unless:
1. You have explicit approval from your team lead
2. There's a specific reason to preserve commit history
3. Each commit is meaningful and follows conventions

### Best Practices

1. **Write good commit messages**: Even with squash merge, good messages help when reviewing PRs
2. **Keep commits atomic**: Each commit should represent a logical change
3. **Don't worry about commit history**: Squash merge will create one clean commit
4. **Focus on PR quality**: The PR description is more important than individual commits

### During PR Review

When reviewing a PR:
- Review the overall changes, not individual commits
- The PR description should explain what changed
- Individual commits are less important with squash merge

### After Merge

After your PR is merged with squash merge:
- Your feature appears as one commit on the target branch
- The commit message should be clear and descriptive
- You can reference the PR number for more details

## Examples

### Example 1: Feature Branch (Squash Merge)

**Feature branch commits:**
```
feat: add shopping cart
fix: resolve cart calculation bug
test: add cart tests
docs: update cart API docs
```

**After squash merge:**
```
feat: add shopping cart functionality

- Implement cart service with add/remove items
- Fix calculation bug for multiple items
- Add comprehensive unit tests
- Update API documentation

Closes #456
```

### Example 2: Bug Fix (Squash Merge)

**Bug fix commits:**
```
fix: resolve payment timeout
fix: add retry logic
test: add timeout tests
```

**After squash merge:**
```
fix: resolve payment gateway timeout

- Fix connection pool configuration
- Add retry logic with exponential backoff
- Add tests for timeout scenarios

Fixes #789
```

## Quick Reference

### Default Strategy
- **Squash Merge**: Use for all feature branches ✅

### Rare Strategy
- **Rebase Merge**: Only with team lead approval ⚠️

### Not Used
- **Create Merge Commit**: Not used at MetaBotX ❌

## FAQ

### Q: Why does MetaBotX prefer squash merge?

**A:** Squash merge creates a clean, readable history where each feature is one commit. This makes it easier to understand project evolution and revert changes if needed.

### Q: When would I use rebase merge?

**A:** Rebase merge is rarely used. Only use it if you need to preserve individual commit history and have explicit approval from your team lead.

### Q: What if my commits aren't perfect?

**A:** That's fine! With squash merge, you can write one comprehensive commit message that describes the entire feature. Focus on making your PR description clear.

### Q: Can I change the commit message when squashing?

**A:** Yes! When you squash merge, GitHub allows you to edit the commit message. Make sure it follows conventional commit format and clearly describes the changes.

## Summary

- **Default**: Use Squash Merge for all PRs ✅
- **Rare**: Use Rebase Merge only with approval ⚠️
- **Never**: Don't use Create Merge Commit ❌
- **Focus**: Write clear PR descriptions, not perfect commits

---

**Next Steps**: Review [Pull Requests Guide](pull-requests.md) to learn how to create effective PRs that will be merged using these strategies.

