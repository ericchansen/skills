---
name: git-commit-message
description: Expert guidance for writing professional Git commit messages following industry best practices. Use when writing commit messages, reviewing commits, or when asked about commit message standards, conventions, or how to improve commit quality.
---

# Git Commit Message Best Practices

Follow these seven rules from Chris Beams' authoritative guide to write commit messages that communicate context effectively to collaborators and your future self.

## The Seven Rules

### 1. Separate subject from body with a blank line
Place a blank line between the subject and body. Git uses this to distinguish the commit title from the description in commands like `git log --oneline` and `git shortlog`.

### 2. Limit the subject line to 50 characters
Aim for 50 characters (soft limit). Maximum 72 characters (hard limit). GitHub truncates subjects longer than 72 characters with an ellipsis.

### 3. Capitalize the subject line
Begin all subject lines with a capital letter.

### 4. Do not end the subject line with a period
Trailing punctuation wastes space. Subject lines should be terse.

### 5. Use the imperative mood in the subject line
Write as if giving a command or instruction: "Fix bug" not "Fixed bug" or "Fixes bug".

**Validation test:** "If applied, this commit will _[your subject line here]_"

This matches Git's own conventions (e.g., "Merge branch 'feature'" or "Revert 'Add feature'").

### 6. Wrap the body at 72 characters
Hard-wrap body text at 72 characters so Git can indent text while keeping total width under 80 columns in terminals.

### 7. Use the body to explain what and why vs. how
The diff shows what changed. The commit body should explain:
- What problem this commit solves
- Why this change is necessary
- Why this solution was chosen over alternatives
- Any side effects or unintuitive consequences

The code itself shows how the change was implemented.

## Commit Message Template

```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

## Common Imperative Verbs

Start your subject line with one of these verbs:

- **Add** - New features, files, or tests
- **Fix** - Bug fixes
- **Remove** - Deletion of features, files, or code
- **Update** - Changes to existing features (not bugs)
- **Refactor** - Code restructuring without behavior changes
- **Improve** - Enhancements without changing behavior
- **Document** - Documentation changes
- **Optimize** - Performance improvements
- **Revert** - Reverting previous commits
- **Merge** - Merging branches or pull requests

## Examples

### ✅ Good Examples

**Example 1: Bug fix with context**
```
Fix autofix preflight failures

Autofix preflight aborted in --yes/--dry-run because debug
logging returned non-zero when ACFS_DEBUG was off, missing fix
handlers triggered set -e exits, and autofix helpers resolved
paths against the repo root, causing missing file errors and
misleading log hints early in the run.

Fix debug logging to always succeed, initialize change-recording
state before writes, preserve nounset around associative array
updates, resolve helper paths relative to their own files, and
add the missing existing-installation handler. These changes
enable preflight to run non-interactively and prevent false
failures under set -e.
```

**Example 2: Performance improvement**
```
Add caching to database queries

Application was making redundant database calls for user profile
data on every request, causing 200ms latency on profile pages.

Implement Redis-based caching layer with 5-minute TTL for user
profiles. Cache is invalidated on profile updates. Reduces
profile page load time from 250ms to 50ms in production.
```

**Example 3: Simple one-line commit (no body needed)**
```
Fix typo in installation documentation
```

### ❌ Bad Examples

**Example 1:** `fixed the bug`
- Not capitalized
- Past tense instead of imperative
- Too vague - which bug?

**Example 2:** `Updated user.py, auth.py, and tests.py to fix authentication issues and improve error handling.`
- Over 50 characters (violates rule 2)
- Ends with period (violates rule 4)
- Lists files changed (git diff shows this)
- Doesn't explain why or what the actual problem was

**Example 3:** `changing behavior of X`
- Not capitalized
- Gerund form instead of imperative
- Fails the "If applied, this commit will..." test

## Pre-Commit Checklist

Before committing, verify your message meets all seven rules:

**Subject line:**
- [ ] ≤50 characters (shoot for 50, hard max 72)
- [ ] Capitalized first word
- [ ] No trailing period
- [ ] Uses imperative mood
- [ ] Passes test: "If applied, this commit will _[subject]_"

**Body (if present):**
- [ ] Blank line separates subject from body
- [ ] Lines wrapped at 72 characters
- [ ] Explains what and why (not how)
- [ ] Provides context for future maintainers

## When Writing Commit Messages

1. **Think atomic commits** - One logical change per commit
2. **Re-establish context** - Assume the reader doesn't know the background
3. **Answer "why?"** - The diff shows what changed; explain why it was necessary
4. **Mention alternatives** - If you chose one approach over another, explain why
5. **Include issue references** - Link to tickets at the end of the body

## Why This Matters

A well-crafted commit message:
- Helps future maintainers understand why changes were made
- Makes `git log`, `git blame`, and `git rebase` more useful
- Improves code review quality
- Enables better collaboration
- Serves as project documentation

A project's long-term success depends on maintainability, and the commit log is one of the most powerful tools for maintainers.

## Reference

Based on Chris Beams' definitive guide: https://cbea.ms/git-commit/
