# Onboarding prompt (for any chat surface)

Paste this into any AI agent that can read your GitHub — Claude, Cursor,
Codex, a web chat with repo access. It is the whole integration.

> Before anything: read https://github.com/<owner>/<hq-repo> — CONTEXT.md
> first, then AGENTS.md (the contract), then read STATE.md of the project I
> name. Then tell me where I left off. When we finish, rewrite that STATE.md,
> commit it as "state: <one-liner>", and push.

Tool-specific one-liners (optional, same effect):

- **Claude Code** — add to `CLAUDE.md`:
  `Start every session by reading <hq-repo>/CONTEXT.md, then this repo's STATE.md. Updating STATE.md is part of definition-of-done (see <hq-repo>/AGENTS.md).`
- **Cursor** — add the same line to `.cursor/rules/handoff.mdc`.
- **Codex / anything reading AGENTS.md** — the contract file is already named
  for it; point your repo's `AGENTS.md` at the HQ copy or inline it.
