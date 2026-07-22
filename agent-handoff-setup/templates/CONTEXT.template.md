# CONTEXT: <your name>

## Who
<Name, GitHub handle(s) + emails, one line on what you do. Keep this section
to facts an agent needs to understand and work on these projects.>

## Machines
- **<machine-name>** - <OS>. Clone roots: `<path where repos live>`.
- <Other machines, and how they access work (GitHub only? local clones?)>

## Project registry (live status = each repo's STATE.md, never here)
### <project-name> - <one-line description>
- status: active | repo: github.com/<owner>/<repo>
- local: <absolute path> (<machine-name>)
### <project-name-2> - <one-line description>
- status: active | repo: github.com/<owner>/<repo>
- local: <absolute path> (<machine-name>)

## Handoff model
- This HQ (entry point) repo stores stable project, machine, and instruction
  information. It is where any agent starts reading. It does not carry current
  project status.
- Each project stores current status in a root `STATE.md`: Progress, Now, Next,
  Decisions, Open questions, and Sync.
- An instructed agent with repository access can read the latest pushed HQ
  and project files.
- Git cannot carry unpushed work, running local services, or files outside the
  repository. Record relevant local-only state in `STATE.md` without including
  secrets.

## Conventions
- Session start: verify needed connections per `CONNECTIONS.md`, then read the
  project's `STATE.md`. Update it when work changes code, blockers, decisions,
  or next actions, or stops pending user input.
- Update this file only when projects/machines change or the shared instructions
  changes; current status (branches, PRs, blockers) never lives here.
