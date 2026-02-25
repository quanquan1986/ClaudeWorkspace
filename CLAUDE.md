# CLAUDE.md

This file provides guidance for AI assistants (Claude Code and similar tools) working in this repository.

## Repository Overview

This is the **quanquan1986/ClaudeWorkspace** repository. As of initial setup, this is a freshly initialized workspace with no application code yet. Update this section as the project evolves.

**Remote:** `http://local_proxy@127.0.0.1:23592/git/quanquan1986/ClaudeWorkspace`

---

## Git Workflow

### Branch Naming Convention

All AI-assisted development branches must follow this pattern:

```
claude/<description>-<session-id>
```

Example: `claude/add-claude-documentation-Dnh6w`

> **CRITICAL:** Branches must start with `claude/` and end with the matching session ID. Pushes to incorrectly named branches will fail with HTTP 403.

### Standard Git Operations

**Pushing to remote:**
```bash
git push -u origin <branch-name>
```

**Fetching a specific branch:**
```bash
git fetch origin <branch-name>
```

**If network errors occur during push/pull**, retry up to 4 times with exponential backoff:
- Wait 2s, retry
- Wait 4s, retry
- Wait 8s, retry
- Wait 16s, retry

### Commit Signing

Commits are automatically signed with an SSH key:
- **Signing key:** `/home/claude/.ssh/commit_signing_key.pub`
- **GPG format:** SSH
- **Sign program:** `/tmp/code-sign`
- **Auto-sign:** Enabled (`commit.gpgsign=true`)

Do not use `--no-gpg-sign` or `--no-verify` flags unless explicitly instructed.

### Commit Message Style

Write clear, descriptive commit messages:
- Use the imperative mood: "Add feature" not "Added feature"
- Keep the subject line under 72 characters
- Separate subject from body with a blank line when detail is needed
- Reference issues or context where relevant

---

## Development Environment

- **Platform:** Linux (x86_64)
- **Git user:** Claude (`noreply@anthropic.com`)
- **Working directory:** `/home/user/ClaudeWorkspace`

---

## General Conventions for AI Assistants

### File Editing

- Always read a file before editing it
- Prefer the `Edit` tool over rewriting entire files
- Only create new files when strictly necessary
- Do not add docstrings, comments, or type annotations to code you did not change

### Code Quality

- Avoid over-engineering — implement only what is requested
- Do not add error handling for scenarios that cannot occur
- Do not introduce abstractions for one-time use
- Do not add backwards-compatibility shims for code that has been removed
- Validate only at system boundaries (user input, external APIs)

### Security

- Never introduce SQL injection, XSS, command injection, or other OWASP Top 10 vulnerabilities
- Do not commit secrets, credentials, or `.env` files
- Do not skip commit hooks (`--no-verify`) without explicit user permission

### Reversibility and Blast Radius

Before taking any action, consider:
- **Local, reversible actions** (editing files, running tests): proceed freely
- **Hard-to-reverse or shared-state actions** (force push, dropping databases, closing PRs, sending messages): confirm with the user first

Specific actions that always require user confirmation:
- `git push --force`
- `git reset --hard`
- Deleting files or branches
- Modifying CI/CD pipelines
- Posting to external services

---

## Updating This File

When new code, tooling, or conventions are introduced to this repository, update the relevant sections of this file. Key sections to add or expand as the project grows:

- **Project Architecture** — directory structure, entry points, key modules
- **Development Setup** — how to install dependencies and run the project locally
- **Testing** — how to run tests, test frameworks used, coverage requirements
- **Build & Deployment** — build commands, CI/CD pipeline, deployment targets
- **Code Style & Linting** — formatters, linters, and how to run them
- **Environment Variables** — required env vars and where to configure them
- **Database** — schema management, migrations, how to reset/seed

---

*Last updated: 2026-02-25 — Initial creation for empty workspace.*
