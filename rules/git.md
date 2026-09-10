# Git review checklist

When reviewing commits or repository status, verify the following:

## 1. Local AI privacy
- Ensure AI-specific configuration files (such as `GEMINI.md`, scratch notes) are ignored locally via `.git/info/exclude` rather than committed to public history.
- Keep commits looking clean and handwritten.

## 2. Commit standards
- Verify commit messages follow the Conventional Commits format (`feat: ...`, `fix: ...`, `refactor: ...`, `perf: ...`).
- Ensure each commit represents a coherent, single unit of work.
