# Software Factory (MVP)

One shared factory that builds many separate projects with Claude Code.
Every project lives in `projects/<name>/`. The workflow is in [`CLAUDE.md`](CLAUDE.md).

## How to use

Open Claude Code in this repo and **just describe what you want** in chat, e.g.
"a CLI that converts CSV to JSON". Claude then:

1. asks only the questions that matter (or none),
2. writes `projects/<name>/SPEC.md` and a task list itself,
3. shows you the plan and **waits for your OK**,
4. builds it: code → `tester` (max 3 attempts per task) → check off + commit →
   `reviewer` → fixes → short summary.

Manual commands still exist: `/new-project <name>` (empty project from the template)
and `/build <name>` (build or continue from the first unchecked task).

## What's inside

| Path | What it is |
|---|---|
| `CLAUDE.md` | Orchestrator instructions (workflow + rules) |
| `templates/SPEC.md` | Spec template copied into every new project |
| `.claude/agents/` | Subagents: `planner`, `tester`, `reviewer` |
| `.claude/commands/` | Slash commands: `/new-project`, `/build` |
| `.claude/settings.json` | Permissions: allow edits + npm/npx/node/git add·commit·status·diff; deny `rm -rf`, `git push`, `sudo` |
| `projects/` | Your projects |

Notes:
- Edits outside the repo are not pre-approved, so Claude asks first;
  `blockReadsOutsideWorkingDirectories` stops file reads outside the repo.
- Pushing is always done by you.
- No hooks yet.
