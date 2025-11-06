# Example Branch Names

This document shows good and bad examples of branch naming conventions.

## Good Branch Names

### Feature Branches

```
✅ feature/user-authentication
✅ feature/add-payment-gateway
✅ feature/implement-shopping-cart
✅ feature/user-profile-settings
✅ feature/PROJ-123-add-search-functionality
✅ feature/add-dark-mode-theme
✅ feature/email-notification-system
```

**Why these are good:**
- Clear prefix (`feature/`)
- Descriptive name
- Uses hyphens, not underscores
- Lowercase letters
- Includes ticket number when applicable

### Bug Fix Branches

```
✅ bugfix/login-error-handling
✅ fix/payment-gateway-timeout
✅ fix/PROJ-456-resolve-null-pointer
✅ bugfix/user-registration-validation
✅ fix/database-connection-issue
```

**Why these are good:**
- Clear prefix (`bugfix/` or `fix/`)
- Describes what's being fixed
- Easy to understand purpose

### Hotfix Branches

```
✅ hotfix/critical-security-patch
✅ hotfix/payment-processing-error
✅ hotfix/urgent-database-fix
✅ hotfix/v1.2.1-critical-bug
```

**Why these are good:**
- Clear prefix (`hotfix/`)
- Indicates urgency
- May include version number

### Release Branches

```
✅ release/v1.3.0
✅ release/version-2.0.0
✅ release/v1.2.5-patch
```

**Why these are good:**
- Clear prefix (`release/`)
- Includes version number
- Follows semantic versioning

### Refactoring Branches

```
✅ refactor/authentication-service
✅ refactor/simplify-database-queries
✅ refactor/extract-common-utilities
```

**Why these are good:**
- Clear prefix (`refactor/`)
- Describes what's being refactored

## Bad Branch Names

### Too Vague

```
❌ feature
❌ fix
❌ update
❌ changes
❌ new-feature
❌ bugfix
```

**Why these are bad:**
- Not descriptive
- Don't explain what the branch does
- Can't tell purpose from name

### Personal/Temporary

```
❌ my-branch
❌ johns-work
❌ test-branch
❌ temp
❌ wip
❌ asdf
❌ testing
❌ experiment
```

**Why these are bad:**
- Personal names aren't helpful
- Temporary names become permanent
- Don't describe purpose
- Can cause confusion in team

### Wrong Format

```
❌ feature_user_login        (should use hyphens)
❌ Feature/UserLogin         (should be lowercase)
❌ feature/user-login/        (trailing slash)
❌ feature/user login         (spaces not allowed)
❌ feature/user.login         (should use hyphens)
```

**Why these are bad:**
- Inconsistent formatting
- Can cause issues with Git
- Harder to work with

### Too Long

```
❌ feature/add-user-authentication-with-oauth2-and-social-media-login
❌ fix/resolve-the-payment-gateway-timeout-issue-that-occurs-when
```

**Why these are bad:**
- Too long to read
- Hard to type
- Difficult to reference

### Missing Prefix

```
❌ user-authentication
❌ payment-gateway
❌ login-fix
```

**Why these are bad:**
- Can't tell branch type
- Harder to organize
- Less clear purpose

## Branch Naming Guidelines

### 1. Use Consistent Prefixes

Always use prefixes to indicate branch type:
- `feature/` - New features
- `bugfix/` or `fix/` - Bug fixes
- `hotfix/` - Critical production fixes
- `release/` - Release preparation
- `refactor/` - Code refactoring
- `docs/` - Documentation changes
- `test/` - Test-related changes
- `chore/` - Maintenance tasks

### 2. Use Hyphens, Not Underscores

```
✅ feature/user-login
❌ feature/user_login
```

### 3. Use Lowercase Letters

```
✅ feature/user-authentication
❌ feature/User-Authentication
❌ feature/USER-AUTHENTICATION
```

### 4. Be Descriptive but Concise

```
✅ feature/add-search-functionality
❌ feature/search
❌ feature/add-search-functionality-with-filters-and-sorting
```

### 5. Include Ticket Numbers When Applicable

```
✅ feature/PROJ-123-user-authentication
✅ bugfix/JIRA-456-payment-error
✅ hotfix/GITHUB-789-security-patch
```

### 6. No Special Characters

```
✅ feature/user-authentication
❌ feature/user@authentication
❌ feature/user#authentication
❌ feature/user.authentication
```

### 7. No Spaces

```
✅ feature/user-authentication
❌ feature/user authentication
❌ feature/user  authentication
```

## Real-World Examples

### Example 1: Adding a Feature

**Task:** Add user profile editing functionality
**Good:** `feature/user-profile-editing`
**Bad:** `feature/profile` or `update`

### Example 2: Fixing a Bug

**Task:** Fix payment gateway timeout issue
**Good:** `bugfix/payment-gateway-timeout`
**Bad:** `fix` or `payment-fix`

### Example 3: Critical Production Fix

**Task:** Fix critical security vulnerability
**Good:** `hotfix/critical-security-patch`
**Bad:** `urgent-fix` or `security`

### Example 4: With Ticket Number

**Task:** Implement user authentication (Ticket #123)
**Good:** `feature/PROJ-123-user-authentication`
**Bad:** `feature/123` or `feature/PROJ123auth`

## Quick Reference

### Good Branch Name Pattern

```
<type>/<description>
```

Where:
- `<type>`: feature, bugfix, hotfix, release, refactor, etc.
- `<description>`: concise description using hyphens

### Examples

```
feature/add-user-authentication
bugfix/resolve-payment-timeout
hotfix/critical-security-patch
release/v1.3.0
refactor/simplify-auth-service
```

## Tips

1. **Be consistent**: Follow the same pattern across all branches
2. **Be descriptive**: Someone should understand the branch purpose from the name
3. **Keep it short**: Long names are hard to work with
4. **Use prefixes**: Makes it easy to organize and filter branches
5. **Include ticket numbers**: Helps track work and link to issues
6. **Review before creating**: Check if a similar branch already exists

