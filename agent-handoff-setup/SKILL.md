---
name: agent-handoff-setup
description: Creates files for passing project context between agents through Git. Use when the user wants an HQ project index, per-project STATE.md files, or a setup that reduces repeated project explanations between sessions, tools, or machines. Typical requests include "set up my HQ", "install the handoff system", and "my AI keeps forgetting what I'm working on". For daily use after setup, use agent-handoff instead.
---

# Agent Handoff Setup

This skill creates a file-based handoff for project context. Context can carry
between sessions when agents read the latest synchronized files, then commit
and push relevant updates before handing off. It does not create automatic
model memory.

The system has three parts:

1. **HQ (entry point) repository:** Stores stable information about the user,
   machines, projects, and shared instructions. It is where any agent, on any
   platform, starts reading. Current project status stays elsewhere.
2. **STATE.md:** Stores current work, next actions, decisions, and blockers in
   each project repository. Update it when project state changes.
3. **Shared Git remote:** Stores pushed commits. Agents need repository access,
   instructions to read the files, and a fetch or pull before relying on
   changes made elsewhere.

Use this skill for initial setup or later restructuring. The separate
`agent-handoff` skill handles daily work and should not repeat the setup
interview.

## Step 1: Interview

Ask conversationally and in batches instead of sending a long questionnaire:

1. **Who are you?** Name, GitHub handle(s), one line on what you do.
2. **Machines.** Which computers do you work from, and where do repos live on
   each? Agents need valid local paths.
3. **Projects.** For each active project: name, GitHub repo, local path, one
   line on what it is. Start with two to five active projects.
4. **Connections.** Besides GitHub, what does an agent need to touch? (Issue
   tracker, local dashboard, database, deploy target.) For each: how to verify
   it works, where credentials live. Never ask for credential values.
5. **HQ repo name.** Suggest `hq-entry-point` so the repo's role is visible
   in its own name, and describe it as the "HQ entry point" in the generated
   files. Ask whether it should use an existing repository or a new one.

If the user has already told you some of this in the conversation, don't
re-ask it. Confirm inferred details and ask only for missing information.

## Step 2: Scaffold

Templates live in `templates/` next to this file. Fill them with the
interview answers. Replace every `<placeholder>` and delete sections that do
not apply.

Build the HQ repo:

```
hq-entry-point/
├── README.md          (what this repo is + the onboarding prompt, from PROMPT.template.md)
├── CONTEXT.md         (from CONTEXT.template.md; user, machines, registry)
├── AGENTS.md          (from AGENTS.template.md; shared instructions)
├── CONNECTIONS.md     (from CONNECTIONS.template.md; verification commands)
└── templates/
    └── STATE.template.md   (copy as-is, for creating future STATE.md files)
```

Then, for each registered project the user can reach from this machine,
create a root `STATE.md` from `STATE.template.md`. Fill it from evidence, not
imagination: read the repo's README, run `git log --oneline -15`, look at open
branches. Ask the user to confirm the "Now" and "Next" sections because
repository history may not show current priorities.

Keep `STATE.md` near 2 KB, replace stale information, keep current project
status out of HQ, and record the rationale for decisions.

## Step 3: Wire it up

- `git init` if needed, commit everything, and offer to push. If the user has
  not created the remote repository, walk them through it. Cross-machine
  handoffs require a shared Git remote or another synchronization method.
- Show the onboarding prompt from the generated README and say exactly what
  it does. Another agent can participate only if it can access the repository
  and follows the onboarding instructions.
- Offer the optional per-tool one-liners (CLAUDE.md, Cursor rules, AGENTS.md)
  from PROMPT.template.md for the projects they touch most.

## Step 4: Verify the setup

Test the onboarding prompt in a fresh session. Ask, "where did I leave off?"
If the answer is incomplete, check repository access, the latest pushed
commit, whether the agent read the requested files, and whether `STATE.md`
contains enough context.
