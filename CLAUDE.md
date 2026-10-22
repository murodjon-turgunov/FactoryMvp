# Software Factory — orchestrator instructions

This repo is one shared factory that builds many separate projects.
Each project lives in its own folder: `projects/<name>/`.

## Roles

- **You (the main session)** are the orchestrator **and** the coder.
- Subagents in `.claude/agents/` help you:
  - `planner` — turns the spec into a task list. Writes no code.
  - `tester` — writes and runs tests for one task, reports failures. Does not fix code.
  - `reviewer` — reviews the finished project with fresh eyes. Does not edit code.

## Workflow: building a project

1. **Read** `projects/<name>/SPEC.md` (and `projects/<name>/CLAUDE.md` if it exists).
   If the spec is still the empty template, stop and ask me to fill it in.
2. **Plan.** Call the `planner` subagent → it writes `projects/<name>/tasks.md`,
   a checklist of small, ordered, testable tasks.
3. **For each task, in order:**
   1. Write the code for this task only.
   2. Call the `tester` subagent with the project name and the task.
   3. Tests fail → fix the code and call the tester again.
      **Max 3 attempts per task.** After the 3rd failure, stop and ask me
      (show the task, what failed, and what you tried).
   4. Tests pass → check the task off in `tasks.md` (`- [ ]` → `- [x]`) and make a git commit:
      `git add projects/<name>` then `git commit -m "<name>: <task>"`.
4. **Review.** When all tasks are done, call the `reviewer` subagent.
   Fix everything it marks as **important** (re-run the tester after the fixes, then commit).
5. **Summary.** Give me a short summary: what was built, how to run it, how to run the
   tests, and anything the reviewer flagged that you did not fix.

## Rules

- Never say "done" unless the tests actually ran and passed. Show the real result.
- Never touch files outside the current project folder `projects/<name>/`.
  (The factory files — this file, `templates/`, `.claude/` — change only when I ask.)
- Keep code simple: the smallest thing that meets the spec. No extra features.
- Never `git push`. I push myself.
