# Example PR Description

This is an example of a well-written Pull Request description following our template.

## Description

This PR implements user authentication functionality using OAuth2 with Google and GitHub as providers. The implementation includes token refresh mechanism, error handling, and proper session management. This addresses the requirement to allow users to sign in with their existing social media accounts instead of creating new credentials.

## Type of Change

- [x] New feature (non-breaking change which adds functionality)
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Refactoring (no functional changes)
- [ ] Performance improvement
- [ ] Chore (build process, dependencies, etc.)

## Changes Made

- Added `AuthService` class to handle authentication logic
- Implemented OAuth2 flow for Google and GitHub providers
- Created `TokenRefreshService` for automatic token refresh
- Added authentication middleware to protect routes
- Created user session management with Redis
- Added error handling for authentication failures
- Updated API documentation with new authentication endpoints

## Testing Performed

- [x] Unit tests added/updated
- [x] Integration tests added/updated
- [x] Manual testing performed
- [x] Tested in [environments/browsers]

**Testing details:**
- Added unit tests for `AuthService` (95% coverage)
- Integration tests for OAuth2 flow with mock providers
- Manual testing with real Google and GitHub accounts
- Tested token refresh flow
- Tested error scenarios (invalid tokens, expired tokens, provider errors)
- Tested in Chrome, Firefox, and Safari browsers
- Verified session management in development and staging environments

## Checklist

- [x] Code follows project style guidelines
- [x] Self-review completed
- [x] Comments added for complex logic
- [x] Documentation updated (if needed)
- [x] No new warnings generated
- [x] Tests added/updated and passing
- [x] All CI/CD checks passing
- [x] No breaking changes (or breaking changes documented)

## Screenshots (if applicable)

### Login Screen
![Login Screen](https://example.com/screenshots/login.png)

### OAuth Provider Selection
![OAuth Selection](https://example.com/screenshots/oauth-selection.png)

## Related Issues/Tickets

- Closes #123
- Related to #456
- Implements requirement from #789

## Breaking Changes

N/A - This is a new feature that doesn't affect existing functionality.

## Additional Notes

- **Dependencies added**: 
  - `oauth2-client` v2.1.0
  - `redis-client` v1.5.0
  
- **Configuration required**: 
  - Add Google OAuth credentials to environment variables
  - Add GitHub OAuth credentials to environment variables
  - Configure Redis connection for session storage
  
- **Migration needed**: 
  - No database migration required for this feature
  
- **Performance considerations**: 
  - Token refresh uses background job to avoid blocking requests
  - Session data stored in Redis for fast access
  
- **Security considerations**: 
  - All tokens are encrypted before storage
  - Tokens expire after 1 hour (configurable)
  - Refresh tokens expire after 30 days

---

**Reviewer Notes:**
- Please test with your own Google/GitHub accounts
- Verify that environment variables are properly documented
- Check that error handling covers all edge cases

