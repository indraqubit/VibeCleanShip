# 📋 Git Commit Best Practices

> **"A well-crafted commit message is a love letter to your future self."**

---

## 🎯 Table of Contents

- [Why Commit Messages Matter](#why-commit-messages-matter)
- [Commit Message Structure](#commit-message-structure)
- [Conventional Commits](#conventional-commits)
- [The Seven Rules](#the-seven-rules)
- [Vibe Coding Integration](#vibe-coding-integration)
- [Common Patterns](#common-patterns)
- [Anti-Patterns to Avoid](#anti-patterns-to-avoid)
- [Tools and Automation](#tools-and-automation)

---

## 💡 Why Commit Messages Matter

Commit messages are **permanent documentation** that explain:

1. **What** changed in the codebase
2. **Why** the change was necessary
3. **How** it relates to the overall project

Good commit messages:
- ✅ Help teammates understand changes quickly
- ✅ Make code reviews more efficient
- ✅ Simplify debugging when things break
- ✅ Generate meaningful changelogs automatically
- ✅ Document the evolution of your thinking
- ✅ Enable effective use of `git blame`, `git log`, and `git bisect`

Bad commit messages:
- ❌ Waste time as developers dig through code to understand intent
- ❌ Make reverting changes risky and unclear
- ❌ Create confusion during debugging sessions
- ❌ Generate useless changelogs

---

## 📝 Commit Message Structure

### Basic Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Detailed Breakdown

#### 1. **Type** (Required)
Indicates the nature of the change:

- `feat` - New feature for the user
- `fix` - Bug fix for the user
- `docs` - Documentation changes
- `style` - Code style changes (formatting, missing semicolons, etc.)
- `refactor` - Code change that neither fixes a bug nor adds a feature
- `perf` - Performance improvements
- `test` - Adding or updating tests
- `build` - Changes to build system or dependencies
- `ci` - Changes to CI/CD configuration
- `chore` - Other changes that don't modify src or test files
- `revert` - Reverts a previous commit
- `vibe` - Experimental/exploratory work (Vibe Coding specific)

#### 2. **Scope** (Optional)
The area of the codebase affected:

- `(auth)` - Authentication module
- `(api)` - API endpoints
- `(ui)` - User interface
- `(db)` - Database
- `(config)` - Configuration files
- `(deps)` - Dependencies

#### 3. **Subject** (Required)
A concise description of the change:

- Use imperative mood: "add" not "added" or "adds"
- Don't capitalize the first letter
- No period at the end
- Limit to 50-72 characters
- Be specific and clear

#### 4. **Body** (Optional)
Detailed explanation of the change:

- Explain **why** not **what** (the diff shows what)
- Wrap at 72 characters per line
- Use bullet points for multiple items
- Include motivation for the change
- Contrast with previous behavior

#### 5. **Footer** (Optional)
Additional metadata:

- Reference issues: `Closes #123`, `Fixes #456`
- Breaking changes: `BREAKING CHANGE: ...`
- Co-authors: `Co-authored-by: Name <email@example.com>`

---

## 🎨 Conventional Commits

[Conventional Commits](https://conventionalcommits.org/) is a specification for structured commit messages.

### Examples

#### ✅ Excellent Commits

```bash
feat(auth): implement JWT-based authentication

Replace session-based auth with JWT tokens to improve scalability
and enable stateless API architecture. This allows horizontal scaling
of the backend without session storage requirements.

- Add JWT token generation and validation
- Update login endpoint to return JWT tokens
- Add middleware for token verification
- Update user authentication flow

Closes #234
```

```bash
fix(api): prevent SQL injection in user search endpoint

Add parameterized queries to user search to prevent SQL injection
attacks. The previous implementation concatenated user input directly
into SQL queries, creating a critical security vulnerability.

SECURITY: This fixes a critical SQL injection vulnerability
```

```bash
refactor(dashboard): extract metrics calculation to separate service

Move complex metrics calculations from the dashboard component to a
dedicated MetricsService. This improves testability, reduces component
complexity, and makes metrics reusable across the application.

- Create MetricsService with unit tests
- Update Dashboard component to use service
- Add caching for expensive calculations
```

#### ✅ Good Commits (Minimal)

```bash
feat(ui): add dark mode toggle
```

```bash
fix(cart): correct tax calculation for international orders
```

```bash
docs(readme): update installation instructions
```

```bash
test(auth): add integration tests for login flow
```

#### ❌ Bad Commits

```bash
# Too vague
git commit -m "fix bug"
git commit -m "update"
git commit -m "changes"

# Not imperative
git commit -m "fixed the login issue"
git commit -m "adding new feature"

# Too detailed in subject
git commit -m "fix the bug where users couldn't login when they had special characters in their password because the validation regex was incorrect"

# No context
git commit -m "WIP"
git commit -m "asdf"
git commit -m "oops"
```

---

## 📏 The Seven Rules

Based on [Chris Beams' guide](https://chris.beams.io/posts/git-commit/):

### 1. Separate subject from body with a blank line

```bash
# Good
feat(api): add user profile endpoint

This endpoint returns user profile information including name,
email, and preferences.
```

### 2. Limit the subject line to 50 characters

```bash
# Good
feat(auth): add password reset flow

# Too long (avoid)
feat(auth): add comprehensive password reset flow with email verification and security questions
```

### 3. Capitalize the subject line

```bash
# Convention varies - we prefer lowercase for type/scope
feat(api): add endpoint
# But capitalize the description part
feat(api): Add user profile endpoint
```

### 4. Do not end the subject line with a period

```bash
# Good
fix(ui): correct button alignment

# Bad
fix(ui): correct button alignment.
```

### 5. Use the imperative mood in the subject line

```bash
# Good
feat: add email validation
fix: prevent memory leak
refactor: extract utility functions

# Bad
feat: added email validation
fix: preventing memory leak
refactor: extracted utility functions
```

**Think**: "If applied, this commit will **[your subject line]**"

### 6. Wrap the body at 72 characters

```bash
feat(dashboard): add real-time metrics display

Implement WebSocket-based real-time metrics for the admin
dashboard. This replaces the previous polling mechanism which
was inefficient and caused unnecessary server load.

Key changes:
- Add WebSocket connection handler
- Implement metrics streaming service
- Update dashboard component for real-time updates
- Add reconnection logic for reliability
```

### 7. Use the body to explain what and why vs. how

```bash
# Good - Explains why
fix(cache): clear cache on user logout

Previous implementation kept cache entries after logout, which
could expose user data if another user logged in on the same
device. Now explicitly clearing cache on logout for security.

# Bad - Only explains what (which the diff already shows)
fix(cache): call clearCache() in logout function
```

---

## 🎵 Vibe Coding Integration

### Commit Workflow Phases

#### Phase 1: Vibe Coding 🎵 (Exploration)

Use `vibe:` prefix for experimental commits:

```bash
vibe: experiment with state management approaches
vibe: add initial dashboard layout
vibe: try different API structures
vibe: prototype user authentication flow
```

**Characteristics**:
- Frequent, quick commits
- May include incomplete features
- Focus on iteration speed
- OK to have "WIP" style messages with vibe: prefix
- These commits will be cleaned up later

#### Phase 2: Reality Check ⚠️

```bash
test: verify login flow works end-to-end
fix: correct validation errors in signup form
```

#### Phase 3: Cleanup 🏗️

Clean up vibe commits before merging:

```bash
# Interactive rebase to squash vibe commits
git rebase -i main

# Example: squash these vibe commits
vibe: add dashboard component
vibe: add metrics display
vibe: fix layout issues
vibe: add charts

# Into a single, meaningful commit
feat(dashboard): implement admin dashboard with real-time metrics
```

#### Phase 4: Production Ready ✅

Final commits should be clean and conventional:

```bash
feat(dashboard): implement admin dashboard with real-time metrics

Add comprehensive admin dashboard with WebSocket-based real-time
metrics, interactive charts, and responsive layout.

Features:
- Real-time metrics updates via WebSocket
- Interactive charts using Chart.js
- Responsive grid layout
- Export functionality for reports

Closes #156
```

### Vibe Commit Guidelines

**During vibe phase, it's OK to**:
- ✅ Make frequent commits with minimal messages
- ✅ Use `vibe:` prefix to mark experimental work
- ✅ Commit incomplete features
- ✅ Have commits that don't build/pass tests

**Before merging to main, you MUST**:
- ✅ Squash vibe commits into logical units
- ✅ Write proper conventional commit messages
- ✅ Ensure all tests pass
- ✅ Remove debug commits that add no value

---

## 🎯 Common Patterns

### Feature Development

```bash
feat(module): add new feature

# Body explains context and impact
# Footer links to issue
```

### Bug Fixes

```bash
fix(component): resolve specific issue

# Body explains the problem and solution
# Footer references the bug report
```

### Breaking Changes

```bash
feat(api)!: change authentication endpoint structure

BREAKING CHANGE: The /auth/login endpoint now returns tokens in
a different format. Clients must update to use the new structure:

Before: { token: "..." }
After: { accessToken: "...", refreshToken: "..." }

Migration guide: docs/migrations/v2-auth.md

Closes #234
```

### Documentation

```bash
docs(readme): update setup instructions

# Simple, clear description of what changed
```

### Refactoring

```bash
refactor(services): extract common logic to shared utilities

# Explain the motivation for the refactoring
# What problems it solves
```

### Performance

```bash
perf(api): optimize database queries in user search

Reduce query time from ~500ms to ~50ms by adding proper indexes
and using query optimization techniques.

- Add composite index on users(email, status)
- Use SELECT only needed columns
- Implement query result caching
```

### Dependencies

```bash
build(deps): upgrade react to v18.2.0

# Include reason if significant
# Note any breaking changes or migration steps
```

---

## ⚠️ Anti-Patterns to Avoid

### 1. Vague Messages

```bash
# Bad
git commit -m "fix"
git commit -m "update"
git commit -m "changes"
git commit -m "stuff"

# Good
git commit -m "fix(auth): prevent token expiration edge case"
```

### 2. Giant Commits

```bash
# Bad - Too many unrelated changes
git commit -m "Add feature X, fix bugs Y and Z, refactor module A, update docs"

# Good - Separate commits
git commit -m "feat(x): add feature X"
git commit -m "fix(y): resolve bug Y"
git commit -m "fix(z): resolve bug Z"
git commit -m "refactor(a): simplify module A"
git commit -m "docs: update API documentation"
```

### 3. Committing Commented-Out Code

```bash
# Bad - Don't commit commented code
git add file-with-commented-code.js
git commit -m "refactor: clean up code"

# Good - Delete it (Git preserves history)
# Remove commented code, commit the clean version
```

### 4. Committing TODO Comments Without Context

```bash
# Bad
// TODO: fix this
// HACK: temporary solution

# Good - Include context
// TODO(username): Refactor to use new API after v2.0 release (#123)
// HACK(username): Temporary workaround for IE11 bug (remove after IE11 support ends)
```

### 5. Mixed Concerns

```bash
# Bad - Multiple unrelated changes
git commit -m "Add login feature and fix typo in README"

# Good - Separate commits
git commit -m "feat(auth): add login feature"
git commit -m "docs: fix typo in README"
```

---

## 🛠️ Tools and Automation

### Commit Message Templates

Create a commit template:

```bash
# ~/.gitmessage
<type>(<scope>): <subject>

<body>

<footer>

# Type: feat, fix, docs, style, refactor, perf, test, build, ci, chore, revert, vibe
# Scope: area of codebase (optional)
# Subject: imperative mood, lowercase, no period, max 50 chars
# Body: explain what and why (optional)
# Footer: issues, breaking changes (optional)
```

Configure Git to use it:

```bash
git config --global commit.template ~/.gitmessage
```

### Commit Hooks

Use [Commitlint](https://commitlint.js.org/) to enforce conventions:

```bash
# Install commitlint
npm install --save-dev @commitlint/cli @commitlint/config-conventional

# Configure
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js

# Add to Husky for pre-commit validation
npm install --save-dev husky
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
```

### Conventional Changelog

Generate changelogs from commits:

```bash
npm install --save-dev standard-version

# Generate changelog and bump version
npx standard-version
```

### Git Aliases

Useful aliases for better commit workflow:

```bash
# Add to ~/.gitconfig
[alias]
    # Quick commit with message
    c = commit -m
    
    # Commit with conventional format
    cf = "!f() { git commit -m \"feat($1): $2\"; }; f"
    cx = "!f() { git commit -m \"fix($1): $2\"; }; f"
    cd = "!f() { git commit -m \"docs($1): $2\"; }; f"
    cv = "!f() { git commit -m \"vibe: $1\"; }; f"
    
    # Amend last commit
    amend = commit --amend --no-edit
    
    # View commit log with graph
    lg = log --graph --oneline --decorate --all
```

Usage:

```bash
git cv "experiment with new layout"
git cf auth "add JWT authentication"
git cx api "prevent SQL injection"
```

---

## 📚 Quick Reference

### Commit Type Cheatsheet

| Type | Usage | Example |
|------|-------|---------|
| `feat` | New feature | `feat(api): add user profile endpoint` |
| `fix` | Bug fix | `fix(auth): prevent token expiration issue` |
| `docs` | Documentation | `docs(readme): update setup instructions` |
| `style` | Formatting | `style(css): fix indentation` |
| `refactor` | Code restructuring | `refactor(utils): extract helper functions` |
| `perf` | Performance | `perf(db): optimize query performance` |
| `test` | Tests | `test(auth): add login integration tests` |
| `build` | Build/dependencies | `build(deps): upgrade react to v18` |
| `ci` | CI/CD | `ci(github): add automated testing workflow` |
| `chore` | Maintenance | `chore: update .gitignore` |
| `revert` | Revert commit | `revert: feat(api): add profile endpoint` |
| `vibe` | Experimental | `vibe: try new state management` |

### Commit Message Template

```
<type>(<scope>): <imperative description max 50 chars>

<Detailed explanation of why this change was made, not how>

<Footer with issue references and breaking changes>
```

---

## 🎯 Conclusion

Good commit practices:

1. **Make commits atomic** - One logical change per commit
2. **Write clear messages** - Future you will thank you
3. **Use conventions** - Consistency helps everyone
4. **Clean up before merging** - Squash vibe commits
5. **Link to issues** - Provide context and traceability

**Remember**: Your commit history is permanent documentation. Treat it with respect! 🚀

---

## 📖 Further Reading

- [Conventional Commits](https://conventionalcommits.org/)
- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Commitlint](https://commitlint.js.org/)
- [Semantic Versioning](https://semver.org/)
- [Keep a Changelog](https://keepachangelog.com/)

---

*Made with ❤️ for developers who value clean Git history*
