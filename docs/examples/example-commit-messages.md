# Example Commit Messages

This document shows good and bad examples of commit messages following the Conventional Commits format.

## Good Commit Messages

### Simple Feature

```
feat: add user authentication

Implement OAuth2 login flow with Google and GitHub providers.
Includes token refresh mechanism and error handling.

Closes #123
```

**Why it's good:**
- Clear type (`feat`)
- Descriptive subject (under 50 chars)
- Body explains what and why
- References related issue

### Bug Fix

```
fix(api): resolve database connection timeout

The connection pool was not properly configured, causing timeouts
under high load. Increased pool size and added retry logic.

Fixes #456
```

**Why it's good:**
- Type and scope clearly indicated
- Subject describes the fix
- Body explains the cause and solution
- Links to issue

### Documentation Update

```
docs: update API documentation for user endpoints

Add examples for all user CRUD operations and error responses.
Include authentication requirements for each endpoint.

Related to #789
```

**Why it's good:**
- Clear type (`docs`)
- Descriptive subject
- Body explains what was added
- Links to related issue

### Refactoring

```
refactor(auth): simplify token validation logic

Extract token validation into separate service class.
Improves testability and reduces code duplication.

No functional changes.
```

**Why it's good:**
- Type and scope specified
- Clear subject
- Body explains the improvement
- Notes no functional changes

### Breaking Change

```
feat(api): change user endpoint response format

BREAKING CHANGE: User endpoint now returns nested user object
instead of flat structure. Update clients to use user.data format.

Migration:
- Old: response.email
- New: response.user.data.email

Closes #234
```

**Why it's good:**
- Clearly marked as breaking change
- Explains what changed
- Provides migration path
- Links to issue

### Performance Improvement

```
perf(database): optimize user query with index

Add database index on user.email column to improve query
performance. Query time reduced from 500ms to 50ms.

Fixes #567
```

**Why it's good:**
- Type indicates performance focus
- Subject describes the optimization
- Body includes measurable improvement
- Links to issue

### Multiple Related Changes

```
feat: add shopping cart functionality

- Implement cart service with add/remove items
- Add cart persistence to database
- Create cart API endpoints
- Add cart UI components

Closes #890
```

**Why it's good:**
- Single commit for related feature
- Bullet points for multiple changes
- Links to issue

### With Scope

```
feat(auth): add password reset functionality

Implement password reset flow with email verification.
Includes token generation, email sending, and password update.

Closes #111
```

**Why it's good:**
- Scope (`auth`) indicates area
- Clear subject
- Body explains implementation
- Links to issue

## Bad Commit Messages

### Too Vague

```
❌ update
❌ fix
❌ changes
❌ WIP
```

**Why they're bad:**
- No type indicated
- No description
- Impossible to understand what changed

### Not Descriptive

```
❌ fix bug
❌ add feature
❌ update code
❌ fix stuff
```

**Why they're bad:**
- Too generic
- Don't explain what was fixed/added
- No context

### Wrong Format

```
❌ Fixed the bug
❌ Added new feature
❌ Updated code to fix issue
```

**Why they're bad:**
- Past tense (should be imperative)
- No type prefix
- Not following conventional format

### Too Long Subject

```
❌ feat: add user authentication with OAuth2 Google GitHub email verification and password reset
```

**Why it's bad:**
- Subject too long (over 50 chars)
- Should be in body instead

### Missing Type

```
❌ user authentication added
❌ fixed payment bug
❌ updated documentation
```

**Why they're bad:**
- No type prefix
- Not following conventional format
- Harder to parse automatically

### Personal/Temporary

```
❌ my changes
❌ testing
❌ asdf
❌ oops
```

**Why they're bad:**
- Not professional
- No information about changes
- Can't understand purpose

## Comparison Examples

### Example 1: Feature Addition

**Bad:**
```
❌ add login
❌ Added user login feature
❌ feat: login
```

**Good:**
```
✅ feat: add user authentication with OAuth2

Implement OAuth2 login flow with Google and GitHub providers.
Users can now sign in with their social media accounts instead
of creating new credentials.

Closes #123
```

### Example 2: Bug Fix

**Bad:**
```
❌ fix bug
❌ Fixed the issue
❌ fix: bug fix
```

**Good:**
```
✅ fix(api): resolve payment gateway timeout

The payment gateway was timing out due to incorrect connection
pool configuration. Increased pool size from 10 to 50 and added
retry logic with exponential backoff.

Fixes #456
```

### Example 3: Refactoring

**Bad:**
```
❌ refactor
❌ code cleanup
❌ refactor: stuff
```

**Good:**
```
✅ refactor(auth): extract token validation to service

Move token validation logic from middleware to dedicated
TokenValidationService. This improves testability and makes
the code more maintainable.

No functional changes.
```

### Example 4: Documentation

**Bad:**
```
❌ docs
❌ updated readme
❌ docs: update
```

**Good:**
```
✅ docs: update API documentation for user endpoints

Add request/response examples for all user CRUD operations.
Include error response formats and status codes.
Document authentication requirements.

Related to #789
```

## Commit Message Templates

### Feature Template

```
feat(<scope>): <subject>

<what was added and why>

Closes #<issue>
```

### Bug Fix Template

```
fix(<scope>): <subject>

<what was wrong and how it was fixed>

Fixes #<issue>
```

### Refactoring Template

```
refactor(<scope>): <subject>

<what was refactored and why>

No functional changes.
```

### Breaking Change Template

```
feat(<scope>): <subject>

BREAKING CHANGE: <what broke>

<migration path>

Closes #<issue>
```

## Quick Reference

### Good Commit Message Checklist

- [ ] Type is correct (feat, fix, docs, etc.)
- [ ] Scope included if applicable
- [ ] Subject is clear and under 50 characters
- [ ] Uses imperative mood
- [ ] Body explains why (if needed)
- [ ] References related issues
- [ ] No unnecessary words
- [ ] Follows conventional commits format

### Type Quick Reference

| Type | Use When | Example |
|------|----------|---------|
| `feat` | New feature | `feat: add user login` |
| `fix` | Bug fix | `fix: resolve null pointer` |
| `docs` | Documentation | `docs: update README` |
| `style` | Formatting | `style: format with black` |
| `refactor` | Refactoring | `refactor: simplify auth` |
| `perf` | Performance | `perf: optimize query` |
| `test` | Tests | `test: add user tests` |
| `chore` | Maintenance | `chore: update deps` |
| `ci` | CI/CD | `ci: add GitHub Actions` |
| `build` | Build system | `build: update webpack` |
| `revert` | Revert | `revert: revert feat X` |

## Tips

1. **Write as if explaining to future you**: You'll thank yourself later
2. **Be consistent**: Use the same format across all commits
3. **Review before committing**: Read your message before finalizing
4. **Think atomic**: One logical change per commit
5. **Reference issues**: Always link related issues/tickets
6. **Use present tense**: "Add feature" not "Added feature"
7. **Don't be afraid to amend**: Fix typos with `git commit --amend`

