---
description: Build projects/<name> with the full factory workflow (plan → code → test → review)
argument-hint: <name>
---

Build the project `projects/$ARGUMENTS/`.

If `$ARGUMENTS` is empty or `projects/$ARGUMENTS/` does not exist, stop and tell me
to run `/new-project <name>` first.

Otherwise follow the **Workflow: building a project** section of the root `CLAUDE.md`
exactly, step by step, and obey its **Rules**. Work only inside `projects/$ARGUMENTS/`.

If `projects/$ARGUMENTS/tasks.md` already exists, do not re-plan: continue from the
first unchecked task.
