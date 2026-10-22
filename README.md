# Software Factory (MVP)

One shared factory that builds many separate projects with Claude Code.
Every project lives in `projects/<name>/`. The workflow is in [`CLAUDE.md`](CLAUDE.md).

## How to use

Open Claude Code in this repo's root folder, then:

1. **`/new-project <name>`** — creates `projects/<name>/` with `SPEC.md`, `CLAUDE.md`,
   `src/` and `tests/`.
2. Fill in `projects/<name>/SPEC.md` (goal, features, tech stack, out of scope,
   definition of done).
3. **`/build <name>`** — runs the whole workflow:
   `planner` writes `tasks.md` → for each task: code → `tester` (max 3 attempts) →
   check off + git commit → `reviewer` → fixes → short summary.

Running `/build <name>` again continues from the first unchecked task in `tasks.md`.

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
