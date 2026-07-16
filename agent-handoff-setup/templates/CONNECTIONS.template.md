# CONNECTIONS - required agent connections (bootstrap contract)

Any agent entering this system verifies the connections its session will need
**before project work**, and troubleshoots failures FIRST so credentials are
never a mid-task barrier. If a fix needs something only the human can issue
(an API key, an OAuth grant, a login), ask immediately and continue with the
surfaces that do work — never silently skip one.

Escalation order per connection: (1) run the verify command, (2) try the
troubleshoot steps, (3) ask the human for the missing credential, (4) record
the gap in the repo's STATE.md `blocked:` if it stops the session's goal.

## 1. GitHub (always required - the cross-agent transport)
- verify: `gh auth status` (expect <your GitHub handle> active)
- troubleshoot: `gh auth login` (web flow), check `git remote -v`,
  token scopes need `repo`

## 2. <Your issue tracker / PM tool, if any>
- key: <where the API key lives — never commit it>
- verify: <one command or check that proves it works>
- troubleshoot: <regenerate key, expected key prefix, settings URL>

## 3. <Local services, if any — dashboards, databases, dev servers>
- verify: <e.g. `curl http://localhost:PORT/health` (any 200 = up)>
- start: <how to start it>

## Secrets
- canonical store: <path to your gitignored secrets file or manager>
- NEVER commit secrets. Other machines: set needed values as env vars.

Update this file whenever a connection is added or changed — it is part of
the global contract.
