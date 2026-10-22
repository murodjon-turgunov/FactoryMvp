---
description: Create a new project in projects/<name> from the spec template
argument-hint: <name>
---

Create a new project named `$ARGUMENTS`.

1. If `$ARGUMENTS` is empty or not a simple folder name (letters, digits, `-`), stop and
   ask me for a name. If `projects/$ARGUMENTS/` already exists, stop and tell me.
2. Create:
   - `projects/$ARGUMENTS/SPEC.md` — a copy of `templates/SPEC.md`, with `<project name>`
     replaced by `$ARGUMENTS`.
   - `projects/$ARGUMENTS/CLAUDE.md` — a short file for project-specific rules:
     ```markdown
     # $ARGUMENTS — project rules

     Rules here apply only to this project and add to the factory's CLAUDE.md.

     - (none yet)
     ```
   - `projects/$ARGUMENTS/src/.gitkeep` and `projects/$ARGUMENTS/tests/.gitkeep`
     (empty folders).
3. Do not write any code and do not commit.
4. Tell me to fill in `projects/$ARGUMENTS/SPEC.md` and then run `/build $ARGUMENTS`.
