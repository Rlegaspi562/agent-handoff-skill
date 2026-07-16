# Onboarding prompt for agents with repository access

Use this prompt with an agent that can access the repository. It tells the
agent which files to read and update.

> First, read https://github.com/<owner>/<hq-repo>, including CONTEXT.md and
> AGENTS.md. Then read STATE.md of the project I name and tell me where the
> work stopped. At the end, update that STATE.md if the session changed code,
> blockers, decisions, or next actions, or stops waiting on my input. If you
> can edit the checkout, commit it as "state: <one-liner>". If the remote
> allows writes, push it.

Optional tool-specific reminders:

- **Claude Code:** add to `CLAUDE.md`:
  `Start every session by reading <hq-repo>/CONTEXT.md, then this repo's STATE.md. Update STATE.md when work changes code, blockers, decisions, or next actions, or stops waiting on user input.`
- **Cursor:** add the same line to `.cursor/rules/handoff.mdc`.
- **Codex or another tool reading AGENTS.md:** the instruction file is already named
  for it; point your repo's `AGENTS.md` at the HQ copy or inline it.

These reminders depend on each tool loading the configured instruction file.
