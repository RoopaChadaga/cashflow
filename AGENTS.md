# Project Memory

## Version control

- This project is versioned in GitHub at https://github.com/RoopaChadaga/cashflow.
- The local Git remote is `origin`, pointing to that repository.
- Use the `main` branch unless the user requests another branch.
- Before substantial or risky edits, create a checkpoint commit.
- After approved changes, run `git add`, `git commit`, and `git push` so the GitHub copy stays current.
- Never use destructive Git commands such as `git reset --hard` or `git checkout --` without explicit user approval.
- When reverting a change, inspect `git log --oneline` first and restore from the selected commit.

## Prototype workflow

- Keep the prototype directly runnable by opening `index.html`.
- Preserve the existing plain HTML, inline CSS, and minimal vanilla JavaScript approach unless the user explicitly requests otherwise.
