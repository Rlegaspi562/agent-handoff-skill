# CONTEXT - <your name> (entry point for all agents)

## Who
<Name, GitHub handle(s) + emails, one line on what you do. Agents read this
first, so keep it to facts an agent needs to act on your behalf.>

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
- HQ (this repo) is the map and global contract. It never carries live
  project status.
- Each project repo owns its current truth in a root `STATE.md`: Progress,
  Now, Next, Decisions, Open questions, Sync.
- GitHub is the cross-agent transport. Any agent with repo access can recover
  the latest pushed handoff from HQ + the named project's `STATE.md`.
- GitHub cannot include unpushed local work, running localhost state, secrets,
  or machine-only files unless an agent records them safely in `STATE.md`.

## Conventions
- Session start: verify needed connections per `CONNECTIONS.md`, then read the
  project's `STATE.md`. Updating STATE.md is part of definition-of-done.
- Update this file only when projects/machines change or the global contract
  changes; live status (branches, PRs, blockers) never lives here.
