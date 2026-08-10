# Security model

Agent Handoff is a set of readable Markdown instructions and templates. It
does not run a background service, collect telemetry, or send project state
to this public repository.

## What the skills may do

When the user asks to set up or run a handoff, the installed skills may direct
an AI agent to:

- read the user's HQ files and project `STATE.md`;
- inspect repository history and connection status;
- create or update handoff files;
- run relevant project checks; and
- commit and push through the Git remote already configured by the user.

The agent's own permission system still controls whether those filesystem,
Git, and network actions are allowed.

## Trust boundaries

- The public package contains blank templates, not a user's private project
  state.
- The generated HQ should be private by default because it may contain
  project names, machine names, and local paths.
- A project's `STATE.md` follows that project's repository permissions. A
  public project has a public `STATE.md` unless the user excludes it.
- Credentials belong in environment variables, a secret manager, or a
  gitignored local file. Handoff files may name where credentials live but
  must never contain their values.
- Agents should collect only the identity, repository, machine, path, and
  connection details required to continue the work.

## Before installing

Read both `SKILL.md` files and the templates. Confirm that the documented Git
operations and file locations match the access you intend to grant your
agent. Use repository credentials with the narrowest permissions that still
support your workflow.

## Reporting a security problem

Do not include credentials, private repository contents, customer data, or
other sensitive values in a public issue. Report the behavior without the
sensitive payload, or contact the maintainer privately through the contact
method listed on the maintainer's GitHub profile.
