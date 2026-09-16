---
applyTo: "**/*.{groovy,Jenkinsfile}"
---

# Jenkins Groovy Instructions

- Prefer declarative Pipeline unless the existing file is scripted Pipeline.
- Keep stages small and clearly named.
- Fail fast and surface actionable errors.
- Do not hide failures with broad `try/catch` unless cleanup or reporting is required.
- Use `withCredentials` for secrets.
- Never echo secrets, tokens, passwords, or credentials.
- Prefer shared library functions if the project already uses them.
- Keep environment variables scoped as tightly as possible.
- Avoid unnecessary agents, workspaces, and duplicated checkout steps.
- Add timeouts around long-running stages.
- Use `post` blocks for cleanup, archiving, and notifications.
- Keep pipelines idempotent and restart-friendly.
- Do not add plugins or shared library dependencies without asking.