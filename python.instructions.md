---
applyTo: "**/*.py"
---

# Python Instructions

- Prefer simple, readable Python over clever abstractions.
- Follow existing project style before introducing new patterns.
- Use type hints for new public functions where useful.
- Avoid new third-party packages unless explicitly approved.
- Prefer standard library solutions first.
- Keep functions small and focused.
- Use explicit exceptions, not broad bare `except`.
- Do not silently ignore errors.
- Add or update tests for behavior changes.
- Preserve CLI behavior and backward compatibility unless asked.
- For command-line scripts, prefer the existing project CLI pattern. If no pattern exists, use `argparse` from the standard library.
- Use clear exit codes and useful stderr messages for automation scripts.