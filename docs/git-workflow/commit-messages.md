# Commit Messages Guide

Clear, well-written commit messages are essential for understanding project history, debugging issues, and collaborating effectively. This guide covers best practices for writing commit messages.

## Why Good Commit Messages Matter

- **Understandability**: Future you (and others) can understand what changed and why
- **Debugging**: Easier to find when bugs were introduced
- **Documentation**: Acts as living documentation of project evolution
- **Collaboration**: Team members can follow your work
- **Automation**: Tools can parse commit messages for changelogs, versioning, etc.

## Conventional Commits Format

We use the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Structure Breakdown

#### Type (Required)
The type of change being made:

- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `style`: Code style changes (formatting, missing semicolons, etc.)
- `refactor`: Code refactoring without functionality changes
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Maintenance tasks, dependency updates, build changes
- `ci`: CI/CD configuration changes
- `build`: Build system or external dependencies
- `revert`: Reverting a previous commit

#### Scope (Optional)
The area of the codebase affected:

```
feat(auth): add OAuth2 login
fix(api): resolve timeout issue
docs(readme): update installation instructions
refactor(utils): simplify helper functions
```

#### Subject (Required)
- Brief description (50 characters or less)
- Use imperative mood ("Add feature" not "Added feature")
- No period at the end
- Capitalize first letter

#### Body (Optional)
- More detailed explanation (wrap at 72 characters)
- Explain what and why, not how
- Separate from subject with blank line

#### Footer (Optional)
- Breaking changes
- Issue references: `Closes #123`, `Fixes #456`

## Examples

### Good Commit Messages

#### Simple Feature
```
feat: add user authentication

Implement OAuth2 login flow with Google and GitHub providers.
Includes token refresh mechanism and error handling.

Closes #123
```

#### Bug Fix
```
fix(api): resolve database connection timeout

The connection pool was not properly configured, causing timeouts
under high load. Increased pool size and added retry logic.

Fixes #456
```

#### Documentation
```
docs: update API documentation for user endpoints

Add examples for all user CRUD operations and error responses.
Include authentication requirements for each endpoint.
```

#### Refactoring
```
refactor(auth): simplify token validation logic

Extract token validation into separate service class.
Improves testability and reduces code duplication.
```

#### Breaking Change
```
feat(api): change user endpoint response format

BREAKING CHANGE: User endpoint now returns nested user object
instead of flat structure. Update clients to use user.data format.

Migration:
- Old: response.email
- New: response.user.data.email
```

#### Multiple Changes
```
feat: add shopping cart functionality

- Implement cart service with add/remove items
- Add cart persistence to database
- Create cart API endpoints
- Add cart UI components

Closes #789
```

### Bad Commit Messages

```
❌ update
❌ fixed bug
❌ changes
❌ WIP
❌ my changes
❌ asdf
❌ fix
❌ Fixed the thing that was broken
❌ Updated code to fix issue #123
```

**Why they're bad:**
- Too vague
- Don't explain what changed
- Don't follow conventional format
- Don't provide context

## Commit Message Best Practices

### 1. Use Imperative Mood

Write commit messages as if completing the sentence: "If applied, this commit will..."

```
✅ feat: add user registration
✅ fix: resolve null pointer exception
✅ docs: update installation guide

❌ feat: added user registration
❌ fix: resolved null pointer exception
❌ docs: updated installation guide
```

### 2. Be Specific and Descriptive

```
✅ feat(auth): add password reset functionality
✅ fix(api): handle null user gracefully in user service
✅ refactor(utils): extract date formatting to helper function

❌ feat: add stuff
❌ fix: fix bug
❌ refactor: refactor code
```

### 3. Keep Subject Line Short

- Aim for 50 characters or less
- Use body for detailed explanation
- If you can't summarize in 50 chars, it might be too many changes

```
✅ feat: add user authentication (28 chars)
✅ fix(api): resolve timeout in payment gateway (42 chars)

❌ feat: add user authentication with OAuth2 Google GitHub and email verification (72 chars - too long!)
```

### 4. Explain the "Why" in Body

```
✅ feat: add user authentication

Implement OAuth2 to reduce password management burden
and improve security. Users can now login with Google,
GitHub, or email.

❌ feat: add user authentication

Added OAuth2 login.
```

### 5. Reference Issues

Link commits to issues/tickets:

```
✅ Closes #123
✅ Fixes #456
✅ Related to #789
✅ See #123 for more context
```

### 6. Use Body for Complex Changes

When the change is complex, use the body to explain:

```
✅ refactor: reorganize project structure

Move all API routes to api/ directory, models to models/,
and services to services/. This improves code organization
and makes the codebase easier to navigate.

Breaking changes:
- Import paths have changed
- Update all imports to new structure
```

## Atomic Commits

### What are Atomic Commits?

Atomic commits are small, focused commits that do one thing well. Each commit should:
- Be a logical unit of change
- Make sense on its own
- Be able to be reverted independently

### Good Atomic Commits

```
feat: add user model
fix: resolve validation error in user model
test: add unit tests for user model
docs: update API docs for user endpoints
```

### Bad (Non-Atomic) Commits

```
❌ feat: add user feature
   (Includes model, API, tests, docs, UI - too much!)

✅ Split into:
   feat: add user model
   feat: add user API endpoints
   test: add user model tests
   docs: update API documentation
```

### Benefits of Atomic Commits

- Easier to review
- Easier to understand
- Easier to revert if needed
- Better git history
- Easier to cherry-pick

## When to Squash Commits

### Squash Before Merging

Squash commits when:
- You have many small "WIP" or "fix typo" commits
- You want to clean up messy commit history
- Your PR has commits that don't make sense individually

### When NOT to Squash

Don't squash when:
- Each commit represents a logical, complete change
- Commits are already well-written and atomic
- You want to preserve detailed history

### How to Squash

**Interactive rebase:**
```bash
# Squash last 3 commits
git rebase -i HEAD~3

# In editor, change "pick" to "squash" for commits to squash
# Save and close, then write new commit message
```

**During PR merge:**
- Use "Squash and merge" option in GitHub
- Write a comprehensive commit message for the squashed commit

## Commit Message Templates

### Git Commit Template

Create `.gitmessage` file:

```
# <type>(<scope>): <subject>
#
# <body>
#
# <footer>
#
# Type can be:
#   feat:     New feature
#   fix:      Bug fix
#   docs:     Documentation changes
#   style:    Code style changes (formatting, etc.)
#   refactor: Code refactoring
#   perf:     Performance improvements
#   test:     Adding/updating tests
#   chore:    Maintenance tasks
#
# Footer can contain:
#   - Breaking changes
#   - Issue references (Closes #123)
```

Configure Git to use it:
```bash
git config --global commit.template .gitmessage
```

### Editor Templates

**VS Code:**
Use extensions like "Conventional Commits" for guided commit messages.

**Vim/Neovim:**
Use plugins like `vim-fugitive` or `nvim-committia`.

## Quick Reference

### Commit Message Checklist

- [ ] Type is correct (feat, fix, docs, etc.)
- [ ] Subject is clear and under 50 characters
- [ ] Uses imperative mood
- [ ] Body explains why (if needed)
- [ ] References related issues
- [ ] No unnecessary words
- [ ] Follows conventional commits format

### Common Commands

```bash
# Commit with message
git commit -m "feat: add user authentication"

# Commit with message and body
git commit -m "feat: add user authentication" -m "Implement OAuth2 login flow"

# Amend last commit message
git commit --amend -m "feat: add user authentication"

# Interactive commit (uses editor)
git commit
```

### Type Quick Reference

| Type | When to Use | Example |
|------|-------------|---------|
| `feat` | New feature | `feat: add user login` |
| `fix` | Bug fix | `fix: resolve null pointer` |
| `docs` | Documentation | `docs: update README` |
| `style` | Formatting | `style: format code with black` |
| `refactor` | Refactoring | `refactor: simplify auth logic` |
| `perf` | Performance | `perf: optimize database query` |
| `test` | Tests | `test: add user service tests` |
| `chore` | Maintenance | `chore: update dependencies` |
| `ci` | CI/CD | `ci: add GitHub Actions workflow` |
| `build` | Build system | `build: update webpack config` |
| `revert` | Revert | `revert: revert user auth feature` |

## Tips

1. **Write as if you're explaining to future you**: You'll thank yourself later
2. **Be consistent**: Use the same format across all commits
3. **Review before committing**: Read your message before finalizing
4. **Think atomic**: One logical change per commit
5. **Reference issues**: Always link related issues/tickets
6. **Use present tense**: "Add feature" not "Added feature"
7. **Don't be afraid to amend**: Fix typos with `git commit --amend`

---

**Next Steps**: Learn about [Code Review Guidelines](../engineering-practices/code-review.md) to understand how your commits will be reviewed.

