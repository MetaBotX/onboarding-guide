# Code Review Guidelines

Code review is a collaborative process where MetaBotX team members review each other's code to ensure quality, share knowledge, and maintain consistency. This guide covers both conducting reviews and receiving feedback.

## What to Review

### Functionality and Correctness

**Questions to ask:**
- Does the code work as intended?
- Are there obvious bugs or edge cases not handled?
- Does it handle error cases properly?
- Are edge cases and boundary conditions considered?
- Does it integrate correctly with existing code?

**Look for:**
- Logic errors
- Missing error handling
- Unhandled edge cases
- Off-by-one errors
- Null pointer exceptions
- Race conditions

### Code Quality and Style

**Questions to ask:**
- Is the code readable and maintainable?
- Does it follow project style guidelines?
- Are there code smells or anti-patterns?
- Is the code well-organized?
- Are naming conventions followed?

**Look for:**
- Meaningful variable and function names
- Consistent formatting
- Proper code organization
- DRY (Don't Repeat Yourself) violations
- Long functions or classes
- Magic numbers or strings

### Test Coverage

**Questions to ask:**
- Are there adequate tests?
- Do tests cover edge cases?
- Are tests clear and maintainable?
- Do tests actually test what they claim to test?
- Is there good test coverage?

**Look for:**
- Unit tests for new functionality
- Integration tests where appropriate
- Test coverage for edge cases
- Clear test names and structure
- Tests that are maintainable

### Documentation

**Questions to ask:**
- Is code well-commented where needed?
- Is documentation updated?
- Are complex algorithms explained?
- Are API changes documented?
- Is README updated if needed?

**Look for:**
- Clear comments for complex logic
- Updated API documentation
- Updated README files
- Inline documentation for public APIs
- Architecture decision documentation

### Performance

**Questions to ask:**
- Are there performance concerns?
- Could this cause memory leaks?
- Are database queries optimized?
- Are there unnecessary computations?
- Is caching used appropriately?

**Look for:**
- N+1 query problems
- Memory leaks
- Inefficient algorithms
- Unnecessary loops
- Missing caching opportunities

### Security

**Questions to ask:**
- Are there security vulnerabilities?
- Is sensitive data handled properly?
- Are inputs validated and sanitized?
- Are authentication/authorization checks in place?
- Are dependencies up to date?

**Look for:**
- SQL injection vulnerabilities
- XSS (Cross-Site Scripting) risks
- Insecure authentication
- Missing authorization checks
- Exposed sensitive data
- Outdated dependencies with known vulnerabilities

## Review Checklist

Use this checklist when reviewing code:

### General
- [ ] Code works as intended
- [ ] Code is readable and maintainable
- [ ] Follows project style guidelines
- [ ] No obvious bugs or errors
- [ ] Error handling is appropriate

### Testing
- [ ] Tests are included for new features
- [ ] Tests cover edge cases
- [ ] Tests are clear and maintainable
- [ ] All tests pass
- [ ] Test coverage is adequate

### Documentation
- [ ] Code is well-commented where needed
- [ ] Documentation is updated
- [ ] Complex logic is explained
- [ ] README updated if needed

### Performance & Security
- [ ] No obvious performance issues
- [ ] No security vulnerabilities
- [ ] Input validation in place
- [ ] Sensitive data handled properly

### Code Quality
- [ ] No code duplication
- [ ] Functions are reasonably sized
- [ ] Naming is clear and consistent
- [ ] Code follows SOLID principles where applicable

## How to Conduct Reviews

### Be Constructive and Respectful

**Good feedback:**
```
✅ "Consider extracting this logic into a separate function for better
   readability. The current function is doing too much."

✅ "This looks good! One small suggestion: we could use a constant
   for the timeout value instead of a magic number."

✅ "I'm not sure I understand this approach. Could you explain the
   reasoning or add a comment?"
```

**Bad feedback:**
```
❌ "This is wrong."
❌ "Why did you do this?"
❌ "This code is terrible."
❌ "You should have done it this way instead."
```

### Explain the "Why" Behind Suggestions

Don't just say what to change, explain why:

```
✅ "Consider using async/await here instead of promises. It makes the
   error handling clearer and the code more readable."

❌ "Use async/await."
```

### Approve vs Request Changes

**Approve when:**
- Code meets all standards
- Only minor suggestions (optional improvements)
- Ready to merge

**Request Changes when:**
- Critical issues need to be fixed
- Functionality doesn't work as expected
- Security concerns
- Missing tests for critical functionality
- Significant style/code quality issues

### Time to Review

- **Timely**: Review within 24-48 hours if possible
- **Prioritize**: Review urgent PRs first
- **Communicate**: If you can't review soon, let the author know
- **Don't rush**: Take time to understand the changes

### Review Process

1. **Understand the context**: Read the PR description first
2. **Review the code**: Go through changes systematically
3. **Test if possible**: Run the code locally if feasible
4. **Provide feedback**: Be specific and constructive
5. **Follow up**: Respond to discussions and questions

## Receiving Reviews

### How to Respond to Feedback

**Accept feedback graciously:**
```
✅ "Thanks for the feedback! I'll update the code."

✅ "Good catch! I'll fix that."

✅ "I've addressed your comments. Let me know if you need
   anything else."
```

**Ask for clarification:**
```
✅ "Could you clarify what you mean by 'simplify this'? Are you
   suggesting a different approach or just refactoring?"

✅ "I'm not sure I understand the concern. Could you elaborate?"
```

### When to Push Back

It's okay to disagree, but do it professionally:

```
✅ "I understand your concern. I chose this approach because [reason].
   However, I'm open to alternatives if you have a better suggestion."

✅ "I see your point, but I think this approach is better because [reason].
   What do you think?"
```

### Keeping Discussions Professional

- **Be respectful**: Even when disagreeing
- **Focus on code**: Not on the person
- **Be open-minded**: Consider alternative approaches
- **Explain your reasoning**: Help reviewers understand your choices
- **Say thank you**: Appreciate the time reviewers spend

### Addressing Feedback

1. **Read all comments**: Don't skip any
2. **Understand the concern**: Ask if unclear
3. **Make changes**: Address the feedback
4. **Respond to comments**: Mark as resolved or explain changes
5. **Re-request review**: When ready for another look

### Example Response Flow

```markdown
# Initial comment from reviewer
@reviewer: "Consider extracting this logic into a helper function."

# Your response after making changes
@author: "Good suggestion! I've extracted the logic into 
         `calculateTotal()` function. Much cleaner now."

# Mark as resolved
✅ Resolved
```

## Common Review Patterns

### Pattern 1: Style Issues

**Reviewer:** "This doesn't follow our style guide. Please use camelCase for function names."

**Author:** "Fixed! Updated all function names to camelCase."

### Pattern 2: Missing Tests

**Reviewer:** "This new feature needs tests. Could you add unit tests?"

**Author:** "Added comprehensive unit tests covering all edge cases."

### Pattern 3: Performance Concern

**Reviewer:** "This query might be slow with large datasets. Consider adding an index or optimizing the query."

**Author:** "Good point. I've optimized the query and added a database index."

### Pattern 4: Security Issue

**Reviewer:** "This input isn't sanitized. Could be a security risk."

**Author:** "Fixed! Added input validation and sanitization."

## Anti-Patterns to Avoid

### As a Reviewer

❌ **Nitpicking**: Don't focus only on minor style issues
❌ **Being vague**: "This could be better" - explain how
❌ **Demanding changes**: Make suggestions, not demands
❌ **Personal attacks**: Focus on code, not the person
❌ **Blocking on minor issues**: Use "Approve with suggestions" for minor things

### As an Author

❌ **Taking feedback personally**: It's about the code, not you
❌ **Ignoring feedback**: Address all comments
❌ **Being defensive**: Be open to suggestions
❌ **Rushing**: Take time to understand and address feedback
❌ **Not asking for clarification**: If unclear, ask!

## Review Best Practices

### For Reviewers

1. **Be kind**: Code review is a learning opportunity
2. **Be specific**: Point to exact lines and explain issues
3. **Be helpful**: Suggest solutions, not just problems
4. **Be timely**: Review within 24-48 hours
5. **Be thorough**: But don't block on minor issues
6. **Be educational**: Use reviews to share knowledge

### For Authors

1. **Be receptive**: Welcome feedback and suggestions
2. **Be responsive**: Address feedback promptly
3. **Be thorough**: Make sure you understand the feedback
4. **Be communicative**: Ask questions if unclear
5. **Be patient**: Reviews take time
6. **Be proactive**: Self-review before requesting review

## Quick Reference

### Review Checklist

- [ ] Code works correctly
- [ ] Code is readable and maintainable
- [ ] Tests are included and passing
- [ ] Documentation is updated
- [ ] No security vulnerabilities
- [ ] No performance issues
- [ ] Follows style guidelines
- [ ] No obvious bugs

### Review Comments Template

```
**Issue:** [What's the problem?]

**Suggestion:** [How to fix it?]

**Reason:** [Why this change?]

**Example:** [Optional code example]
```

### Response Template

```
Thanks for the feedback!

[What you changed]

[How it addresses the concern]

Let me know if you need anything else!
```

## Tips

1. **Start positive**: Acknowledge what's good before suggesting changes
2. **Be specific**: Point to exact lines and explain issues clearly
3. **Suggest, don't demand**: Frame feedback as suggestions
4. **Explain why**: Help authors understand the reasoning
5. **Be timely**: Don't leave PRs waiting for days
6. **Keep it professional**: Focus on code, not people
7. **Learn from reviews**: Use them as learning opportunities

---

**Next Steps**: Review the [Development Workflow](../onboarding/development-workflow.md) to understand the daily development process.

