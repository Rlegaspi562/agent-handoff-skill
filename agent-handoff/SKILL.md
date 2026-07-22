---
name: agent-handoff
description: Runs the daily read, work, checks, state update, handoff verification, and push loop for an existing HQ and STATE.md setup. Use when beginning from a saved handoff or ending work that changed code, decisions, blockers, or next actions. Typical requests include "where did I leave off?", "continue the build", "handoff", and "save state". If the required files do not exist, use agent-handoff-setup instead.
---

# Agent Handoff: daily loop

Follow this sequence: **read, work, run checks, update state, verify the
handoff, and push**. Continuity depends on participating agents reading the
latest pushed `STATE.md` and updating it when the session changes project
state.

## Session start (read)

0. **Orient.** Before touching files, determine which position you are in:
   - **Inside a registered project:** continue with the normal loop below.
   - **Outside any project, or a cross-project question:** read the HQ (entry
     point) repo's `CONTEXT.md` first. Do not create or modify project files
     from unregistered ground.
   - **Creating a new repository, or inside a repo the HQ registry does not
     list:** this is registration, not just building. Before the first commit,
     create the repo's `STATE.md` (from `templates/STATE.template.md`), add a
     registry entry to HQ's `CONTEXT.md` (stable facts only), and add any
     tool-specific pointer files the user uses (see `PROMPT.template.md`).
     Then continue with the build.
1. **Sync.** `git pull` in the project repo (and in HQ if you have it
   locally). Report briefly if the pull isn't a fast-forward.
2. **Verify connections** the session will need, per HQ's `CONNECTIONS.md`.
   Check required credentials before starting dependent work. If only the user
   can restore access, ask before proceeding with that part of the task.
3. **Read the map if needed.** Working in a known project: read its root
   `STATE.md` directly. Cross-project question ("what am I working on?"):
   read HQ's `CONTEXT.md` first, then the STATE.md of each relevant project
   from the registry.
4. **Report position in one paragraph:** current phase, whether anything is
   blocked, the top items from `## Next`, and any open questions waiting on
   the user. No file dumps. Mention a rejected path only if today's work
   risks re-trying it.
5. **Missing STATE.md?** Fall back to `git log --oneline -10` + the repo's
   README, say the file is missing, and offer to create one from HQ's
   `templates/STATE.template.md` at session end.
6. **Check the Sync line.** If it says FAILED, run `git push` now and report.

## Work

Do the session's work as normal. Track these details while working:

- Record decisions, their rationale, and failed approaches that should not be
  repeated.
- Record relevant local-only state, such as unpushed branches, running
  services, incomplete migrations, or files outside the repository.

## Session end: test, update, and push

Update STATE.md **unprompted** whenever the session changed code, added or
removed a blocker, made a decision, changed next actions, or ends waiting on
the user.

1. **Run relevant checks.** Test the code, documentation, or workflow changed
   during the session. Record any failure that remains.
2. **Rewrite** the project's `STATE.md`. Replace stale content instead of
   appending entries. Keep the format (Progress / Now / Next / Decisions /
   Open questions / Sync) and target 2 KB. Fold new decisions into
   `decided/tried/rejected`; replace `## Now`; reorder `## Next` so item 1 can
   begin without conversation history.
3. **Check the handoff.** Reread the file without relying on the current
   conversation. Add any path, command, or context needed to begin the first
   next action.
4. **Commit** as `state: <one-liner>` in the same batch as the session's code
   commits, and **push**. If the push fails, keep the local commit, set the
   Sync line to `last push: <date> | FAILED (<reason>)`, create a second local
   state commit containing that failure record, tell the user, and continue
   with work that does not require the push.
5. **Merge conflict on STATE.md?** Merge the Next lists, keep the newer Now
   and Progress, combine Decisions without duplicates, note the merge under
   `tried:`.

## Repository rules

- Keep current project status in the project repository, not in HQ.
- Record decisions and rationale, not only changed files.
- Long-lived branches can produce conflicting `STATE.md` versions. Avoid
  changing the same subsystem independently on both the feature and default
  branches.
