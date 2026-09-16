---
applyTo: "**/*.{yml,yaml}"
---

# Ansible Instructions

Apply these rules when editing Ansible playbooks, roles, inventories, vars, or molecule files.

- Keep tasks idempotent.
- Prefer built-in Ansible modules over shell or command tasks.
- Use `shell` only when shell features are required.
- Use `command` instead of `shell` when possible.
- Always add `changed_when` and `failed_when` for command-style tasks where needed.
- Avoid hardcoded hosts, users, paths, and credentials.
- Use variables with clear defaults.
- Prefer role defaults over duplicated vars.
- Use handlers for service restarts.
- Do not log secrets. Use `no_log: true` for sensitive values.
- Keep privilege escalation explicit with `become`.
- Preserve inventory and group variable structure.
- Do not introduce collection dependencies without asking.