# CONNECTIONS: required access

Before project work, verify the connections required for the task. If one
fails, try the documented fix. Ask the user when restoring access requires a
credential or login they control. Continue only with work that does not depend
on the failed connection.

For each connection: run the verification command, try the troubleshooting
steps, ask the user when needed, and record the blocker in `STATE.md` if it
prevents the task.

## 1. GitHub, required for hosted synchronization
- verify: `gh auth status` (expect <your GitHub handle> active)
- troubleshoot: `gh auth login` (web flow), check `git remote -v`,
  token scopes need `repo`

## 2. <Your issue tracker / PM tool, if any>
- key: <where the API key lives; never commit it>
- verify: <one command or check that proves it works>
- troubleshoot: <regenerate key, expected key prefix, settings URL>

## 3. <Local services, such as dashboards, databases, or dev servers>
- verify: <e.g. `curl http://localhost:PORT/health`; a 200 response confirms
  that the health endpoint is responding>
- start: <how to start it>

## Secrets
- canonical store: <path to your gitignored secrets file or manager>
- Do not commit secrets. On other machines, provide required values through
  environment variables or the named secret manager.

Update this file whenever a connection is added or changed.
