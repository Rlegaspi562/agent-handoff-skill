# Agent Handoff: Pick Up Where the Last Agent Stopped

Switching sessions, tools, or machines should not mean explaining the whole
project again.

Agent Handoff keeps current project context in plain Markdown and Git so
Claude Code, Codex, Cursor, or another repo-aware agent can continue from the
same handoff:

- An HQ (entry point) repository maps your projects, machines, and shared
  instructions.
- Each project has a compact `STATE.md` with current work, next actions,
  decisions, blockers, and failed approaches worth remembering.
- Git carries the latest pushed handoff between agents and machines.

An agent can continue when it has repository access and follows the handoff
instructions. This is persistent project context, not automatic model memory.

```text
You: Where did I leave off?

Agent: The migration is in review. One Windows test is still failing.
The rejected cache approach is recorded. Next: fix the remaining test.
```

[![Animated walkthrough of the handoff flow](assets/agent-handoff-in-motion.gif)](assets/rumil-agent-handoff-skill.png)

Click the animation to open the full-resolution diagram.

## One public package, private project state

This public repository contains the reusable skills, instructions, and blank
templates. It does not contain a user's private HQ, working project registry,
or real project handoffs.

The root [`STATE.md`](STATE.md) tracks maintenance of this public package
itself. It contains no private project state.

Running the setup creates a separate installation for the user:

- the HQ repository is private by default because it may contain machine
  names, project names, and local paths;
- each `STATE.md` stays with its own project and follows that project's access
  controls; and
- no project state is sent back to this repository.

You do not need separate public and private copies of the skill. Keep this
package public and keep the generated HQ and sensitive project state private.

## What's included

| Piece | What it does |
|---|---|
| [`agent-handoff-setup/`](agent-handoff-setup/) | Asks setup questions, then creates the HQ files and a `STATE.md` for each project |
| [`agent-handoff/`](agent-handoff/) | Handles the session workflow: read context, work, run checks, update state, verify the handoff, and push |
| [`agent-handoff-setup/templates/`](agent-handoff-setup/templates/) | Contains five Markdown templates that can be used without installing the skills |
| `agents/openai.yaml` in each skill | Adds Codex display names, descriptions, and starter prompts |

## Where it fits

Agent Handoff is a continuity layer, not an agent runtime, task manager, or
database. It does not launch agents, isolate worktrees, or claim to give a
model permanent memory. It gives the next agent a small, current record it can
read before continuing.

Hooks are optional. A client-specific hook can remind or require an agent to
read and update the handoff, but the core files remain usable without hooks or
a particular AI client.

## Before you start

You need Git, a place to host or synchronize the repositories, and an AI agent
that can read and write the relevant checkouts. GitHub is convenient, but any
shared Git remote works.

The generated HQ can contain project names, machine names, and local paths.
Keep it **private by default**. Never put passwords, API keys, tokens, or other
credential values in the handoff files.

## Install the skills

Clone this repository first:

```bash
git clone https://github.com/Rlegaspi562/agent-handoff-skill
```

Install both folders together so `agent-handoff` can use the setup templates.

### Claude Code

macOS or Linux:

```bash
mkdir -p ~/.claude/skills
cp -R agent-handoff-skill/agent-handoff-setup agent-handoff-skill/agent-handoff ~/.claude/skills/
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse -Force .\agent-handoff-skill\agent-handoff-setup, .\agent-handoff-skill\agent-handoff "$HOME\.claude\skills\"
```

### Codex

Use the same commands, replacing `.claude/skills` with `.codex/skills`.

Then say: *"Set up my agent handoff system."* The setup skill asks only for
the project details it still needs, creates the HQ files, and creates a
`STATE.md` for each registered project. In later sessions, use *"where did I
leave off?"* to read the handoff and *"handoff"* to save it.

## Using another agent

The files do not require Claude Code. Copy the
[templates](agent-handoff-setup/templates/), fill them in, and push them to a
Git remote. Then give this instruction to an agent with repository access:

> First, read `<your-hq-repo>`. Read `CONTEXT.md`, then `AGENTS.md`, followed
> by the named project's `STATE.md`. Tell me where the project stopped. At the
> end, update `STATE.md` if the session changed code, blockers, decisions, or
> next actions, or stops waiting on my input. If you can edit the checkout,
> commit it as `state: <one-liner>`. If the remote allows writes, push it.

Optional reminders for Cursor, Codex, and Claude Code are in
[`PROMPT.template.md`](agent-handoff-setup/templates/PROMPT.template.md).

## Privacy checklist

Before pushing an HQ repository, confirm that:

- the remote is private unless you deliberately created a redacted public HQ;
- `CONTEXT.md` contains only identifiers, projects, machines, and paths that
  participating agents genuinely need;
- `CONNECTIONS.md` names credential locations or secret managers, never
  credential values; and
- `STATE.md` contains useful work context but no secrets, customer data, or
  private conversation transcripts.

See [`SECURITY.md`](SECURITY.md) for the package's behavior and trust
boundaries.

## Operating rules

1. Keep current project status in each project's `STATE.md`, not in the HQ
   entry point repo.
2. Update `STATE.md` when work changes code, decisions, blockers, or next
   actions.
3. Replace stale information instead of appending a history. Keep the file
   near 2 KB.
4. Record decisions, rationale, and failed approaches that affect future work.
5. Commit and push the handoff when Git write access is available.

## Start small

Start with one `STATE.md` in one repository. Add an HQ (entry point)
repository when you need to track more than one project. The file-based setup
does not require a database or a separate API.

MIT licensed. Built by [Rumil Legaspi](https://github.com/Rlegaspi562).
