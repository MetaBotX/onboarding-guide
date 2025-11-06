# Pull Requests Guide

Pull Requests (PRs) are the primary way code changes are reviewed, discussed, and merged into the codebase. This guide covers everything you need to know about creating effective PRs.

## What is a Pull Request?

A Pull Request is a request to merge changes from one branch into another. It's the mechanism for:
- Code review
- Discussion and collaboration
- Quality assurance
- Documentation of changes

## PR Description Template

Use this template when creating PRs:

```markdown
## Description
Brief description of what this PR does and why it's needed.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Refactoring (no functional changes)
- [ ] Performance improvement
- [ ] Chore (build process, dependencies, etc.)

## Changes Made
- List of specific changes made
- What was added/modified/removed
- Any architectural changes

## Testing Performed
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] Manual testing performed
- [ ] Tested in [environments/browsers]

Describe what testing you've done:
- How you tested the changes
- Test scenarios covered
- Any edge cases tested

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex logic
- [ ] Documentation updated (if needed)
- [ ] No new warnings generated
- [ ] Tests added/updated and passing
- [ ] All CI/CD checks passing
- [ ] No breaking changes (or breaking changes documented)

## Screenshots (if applicable)
Add screenshots for UI changes:

## Related Issues/Tickets
- Closes #123
- Related to #456
- Fixes #789

## Breaking Changes
If this PR introduces breaking changes, describe them here:
- What changed
- Migration path for users
- How to update code

## Additional Notes
Any additional information reviewers should know:
- Dependencies added/removed
- Performance considerations
- Security implications
```

## PR Title Conventions

### Good PR Titles
```
feat: Add user authentication with OAuth2
fix: Resolve payment gateway timeout issue
docs: Update API documentation for user endpoints
refactor: Simplify authentication middleware
chore: Update dependencies to latest versions
```

### Bad PR Titles
```
❌ Update
❌ Fix bug
❌ Changes
❌ WIP
❌ My changes
❌ Latest updates
```

**Guidelines:**
- Use conventional commit format: `type: description`
- Be specific and descriptive
- Keep under 72 characters
- Use imperative mood ("Add feature" not "Added feature")

## Best Practices

### Keep PRs Focused and Small

**Do:**
- ✅ One feature or fix per PR
- ✅ Keep PRs to a reasonable size (< 500 lines ideally)
- ✅ Split large features into multiple PRs

**Don't:**
- ❌ Mix unrelated changes
- ❌ Include "while I was at it" changes
- ❌ Create massive PRs that are hard to review

### Write Clear Commit Messages

Each commit in your PR should have a clear message:
```
✅ feat: Add user login functionality
✅ fix: Resolve null pointer exception in user service
✅ test: Add unit tests for authentication flow
```

### Link to Related Issues

Always link related issues or tickets:
```markdown
## Related Issues
- Closes #123
- Fixes #456
- Related to #789
```

This helps reviewers understand context and automatically closes issues when merged.

### Request Appropriate Reviewers

- Ask team members familiar with the codebase area you're changing
- Include the tech lead or architect for architectural changes
- Tag domain experts for domain-specific changes
- Don't spam the entire team unnecessarily

### Keep PRs Up-to-Date

Regularly update your PR with changes from the base branch:
```bash
# Update your feature branch
git checkout feature/your-feature-name
git pull origin develop  # or git rebase develop
git push origin feature/your-feature-name
```

### Respond to Feedback Promptly

- Address review comments in a timely manner
- Ask for clarification if feedback is unclear
- Push new commits addressing feedback
- Re-request review when ready

## Review Process

### What Reviewers Look For

1. **Functionality**
   - Does the code work as intended?
   - Are there obvious bugs?
   - Does it handle edge cases?

2. **Code Quality**
   - Is the code readable and maintainable?
   - Does it follow project style guidelines?
   - Are there code smells or anti-patterns?

3. **Testing**
   - Are there adequate tests?
   - Do tests cover edge cases?
   - Are tests clear and maintainable?

4. **Documentation**
   - Is code well-commented where needed?
   - Is documentation updated?
   - Are complex algorithms explained?

5. **Performance**
   - Are there performance concerns?
   - Could this cause memory leaks?
   - Are database queries optimized?

6. **Security**
   - Are there security vulnerabilities?
   - Is sensitive data handled properly?
   - Are inputs validated and sanitized?

### How to Address Feedback

1. **Read all comments carefully**
   - Understand what's being asked
   - Don't take feedback personally

2. **Ask for clarification if needed**
   ```markdown
   @reviewer Could you clarify what you mean by "simplify this logic"? 
   Are you suggesting a different approach or just refactoring?
   ```

3. **Make changes and commit**
   ```bash
   # Make your changes
   git add .
   git commit -m "refactor: simplify authentication logic based on review"
   git push origin feature/your-feature-name
   ```

4. **Respond to comments**
   - Mark resolved comments as resolved
   - Explain changes made
   - Discuss if you disagree with feedback

5. **Re-request review when ready**
   - Click "Re-request review" after addressing feedback
   - Add a comment summarizing changes made

### Re-requesting Reviews

After addressing feedback:
1. Push your changes
2. Mark resolved comments
3. Re-request review from reviewers
4. Optionally add a comment: "Addressed all feedback, ready for another review"

### Responding to Comments

**Professional responses:**

```markdown
✅ "Thanks for the feedback! I've refactored the function to be more readable."
✅ "Good catch! I've added validation for edge cases."
✅ "I updated the documentation. Let me know if you need more details."
```

**When you disagree:**

```markdown
✅ "I understand your concern. I chose this approach because [reason]. 
   Would you prefer a different solution? I'm open to suggestions."
```

## PR Lifecycle

### 1. Draft PR (Work in Progress)

Mark PR as draft when:
- Still working on the feature
- Want to share early progress
- Not ready for review yet

```markdown
# Create draft PR
[WIP] Add user authentication

# Or mark existing PR as draft
# Click "Convert to draft" button
```

### 2. Ready for Review

When ready:
- Mark as "Ready for review"
- Ensure all checks pass
- Write a clear description
- Request reviewers

### 3. In Review

During review:
- Respond to comments promptly
- Make requested changes
- Discuss disagreements professionally
- Keep PR updated with base branch

### 4. Approved

After approval:
- Ensure all required approvals are obtained
- Verify all CI/CD checks pass
- Wait for merge (if not auto-merge)

### 5. Merged

After merge:
- PR is closed
- Branch can be deleted
- Changes are in target branch
- Related issues are closed (if linked)

## Merge Strategies

At MetaBotX, we use specific merge strategies to maintain clean project history. See the [Merge Strategies Guide](merge-strategies.md) for complete details.

### Default: Squash and Merge

**Use Squash and Merge for all feature branches.** This is the default strategy at MetaBotX.

- Combines all commits into one clean commit
- Creates readable, linear history
- Makes it easy to understand what each feature does
- Simplifies reverting changes if needed

**When merging your PR:**
1. Select "Squash and merge"
2. Review and edit the commit message if needed
3. Ensure the message follows conventional commit format
4. Click "Confirm squash and merge"

### Rebase and Merge (Rare, Requires Approval)

Rebase and merge is rarely used at MetaBotX. Only use it if:
- You have explicit approval from your team lead
- You need to preserve individual commit history
- Each commit represents a meaningful, standalone change

**Default to squash merge unless specifically requested otherwise.**

### Create a Merge Commit (Not Used)

MetaBotX does not use "Create a Merge Commit" as it clutters history and makes it harder to understand changes.

For complete guidance on merge strategies, see the [Merge Strategies Guide](merge-strategies.md).

## Common PR Mistakes

### ❌ Too Large or Unfocused
**Problem**: PR with 50+ files, multiple unrelated changes
**Solution**: Split into smaller, focused PRs

### ❌ Missing Tests
**Problem**: Code changes without corresponding tests
**Solution**: Always include tests for new features/fixes

### ❌ Vague Description
**Problem**: "Fixed bug" or "Updated code"
**Solution**: Explain what, why, and how

### ❌ Ignoring CI/CD Failures
**Problem**: PR with failing tests or linting
**Solution**: Fix all issues before requesting review

### ❌ Not Updating Base Branch
**Problem**: PR is behind base branch with conflicts
**Solution**: Regularly update and resolve conflicts

### ❌ Not Responding to Feedback
**Problem**: Leaving review comments unanswered
**Solution**: Address all feedback or discuss disagreements

## Quick Reference

### PR Checklist
- [ ] Clear, descriptive title
- [ ] Detailed description using template
- [ ] Related issues linked
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] Code follows style guidelines
- [ ] All CI/CD checks passing
- [ ] Appropriate reviewers requested
- [ ] Branch up-to-date with base branch

### PR Workflow Commands

```bash
# Create PR (after pushing branch)
# Usually done via GitHub UI

# Update PR with latest base branch
git checkout feature/your-feature-name
git pull origin develop
git push origin feature/your-feature-name

# Address feedback and push
git add .
git commit -m "fix: address review feedback"
git push origin feature/your-feature-name
```

## Tips for Effective PRs

1. **Self-review first**: Review your own PR before requesting others
2. **Test thoroughly**: Ensure everything works before requesting review
3. **Be descriptive**: Help reviewers understand context
4. **Keep it small**: Smaller PRs are easier to review and merge faster
5. **Respond promptly**: Don't leave reviewers waiting
6. **Be open to feedback**: Code review is a learning opportunity
7. **Celebrate merges**: Getting a PR merged is an achievement!

---

**Next Steps**: Learn about [Branch Management](branch-management.md) to keep your branches organized.

