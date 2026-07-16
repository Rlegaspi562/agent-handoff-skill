---
name: agent-handoff-setup
description: One-time guided setup that builds a persistent project-context system across AI agents — an HQ map repo plus a STATE.md in every project, with GitHub as the glue. Use when the user wants to set up agent handoffs, stop re-explaining their projects every session, share context between Claude/Cursor/Codex or between machines, or says things like "set up my HQ", "install the handoff system", "my AI keeps forgetting what I'm working on". For the daily loop after setup, use the agent-handoff skill instead.
---

# Agent Handoff — Setup

You are scaffolding a handoff system for someone who is tired of every AI
session starting with amnesia. The claim this system makes is precise:
**persistent project context across agents** — any agent on any machine picks
up where the last one left off, because the context lives in plain markdown in
git, not in any one tool's memory. Do not oversell it as automatic model
memory; it works because agents read and write these files every session.

The system has three parts:

1. **HQ repo** — the map. Stable facts only: who the user is, their machines,
   a registry of their projects, the global contract. Never live status.
2. **STATE.md** — one per project repo, at the root. The live truth: what's
   done, what's next, what was decided and rejected. Rewritten every session.
3. **GitHub** — the transport. If it's pushed, any agent anywhere can read it.

This skill runs ONCE (or when the system needs restructuring). The daily
read/work/update/push loop is the separate `agent-handoff` skill — do not
re-ask setup questions during daily work.

## Step 1: Interview

Ask, conversationally and in batches (not twenty questions one at a time):

1. **Who are you?** Name, GitHub handle(s), one line on what you do.
2. **Machines.** Which computers do you work from, and where do repos live on
   each? (Clone roots matter — agents need real paths.)
3. **Projects.** For each active project: name, GitHub repo, local path, one
   line on what it is. 2-5 projects is the sweet spot to start.
4. **Connections.** Besides GitHub, what does an agent need to touch? (Issue
   tracker, local dashboard, database, deploy target.) For each: how to verify
   it works, where credentials live. Never ask for credential values.
5. **HQ repo name.** Suggest `hq` — short, memorable, easy to type in a
   prompt. Ask where it should live (existing repo? new one?).

If the user has already told you some of this in the conversation, don't
re-ask — confirm what you inferred and fill only the gaps.

## Step 2: Scaffold

Templates live in `templates/` next to this file. Fill them with the
interview answers — replace every `<placeholder>`; delete sections that
genuinely don't apply rather than leaving stubs.

Build the HQ repo:

```
hq/
├── README.md          (what this repo is + the onboarding prompt, from PROMPT.template.md)
├── CONTEXT.md         (from CONTEXT.template.md — who, machines, registry)
├── AGENTS.md          (from AGENTS.template.md — the global contract)
├── CONNECTIONS.md     (from CONNECTIONS.template.md — verify commands)
└── templates/
    └── STATE.template.md   (copy as-is, for creating future STATE.md files)
```

Then, for each registered project the user can reach from this machine,
create a root `STATE.md` from `STATE.template.md`. Fill it from evidence, not
imagination: read the repo's README, run `git log --oneline -15`, look at open
branches. Ask the user to confirm the "Now" and "Next" sections — those are
the two sections only they truly know.

Keep every generated file honest to the format rules: STATE.md targets 2KB
and is rewritten, never appended; live status never goes in HQ; decisions
record *why*, not just *what*.

## Step 3: Wire it up

- `git init` (if new), commit everything, and offer to push. If the user
  hasn't created the GitHub repo yet, walk them through it — the system only
  works once it's pushed.
- Show the onboarding prompt from the generated README and say exactly what
  it's for: paste it into ANY agent with repo access, and that agent joins
  the system. No plugin, no vendor, no lock-in.
- Offer the optional per-tool one-liners (CLAUDE.md, Cursor rules, AGENTS.md)
  from PROMPT.template.md for the projects they touch most.

## Step 4: Prove it

End with a test, not a summary. Tell the user: open a fresh session in a
different tool (or a fresh session here), paste the onboarding prompt, and ask
"where did I leave off?" If the answer is right, the system works. If it
isn't, the gap is in a STATE.md — fix the file, not the agent.
