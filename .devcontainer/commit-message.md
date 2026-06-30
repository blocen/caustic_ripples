---
name: commit-message
description: Generate a commit message for staged changes. Use when asked to write a commit message, suggest a commit message, or create a commit message.
<!-- allowed-tools: Bash -->
---

1. Run `git diff --cached` to see staged changes. If nothing is staged, run `git diff` for unstaged changes.
2. Run `git log --oneline -5` to match the repo's commit style.
3. Write a single Conventional Commits subject line:

```
<type>(<optional scope>): <subject>
```

- Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `ci`
- Subject: imperative mood, max 72 chars, lowercase after the colon
- Add a body only if the why is non-obvious — one short paragraph, blank line after subject

Output the commit message as a fenced code block. Do not run `git commit`.
