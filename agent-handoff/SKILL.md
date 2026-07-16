---
name: agent-handoff
description: The daily loop for a persistent project-context system (HQ repo + per-project STATE.md, GitHub as the glue). Use at the START of any work session — "where did I leave off?", "pick up where we stopped", "continue the build", "what am I working on?" — and at the END of any session that changed code, made a decision, or hit a blocker: "handoff", "save state", "I'm stopping". If the user has no HQ repo or STATE.md files yet, use agent-handoff-setup instead.
---

# Agent Handoff — the daily loop

One repeatable route, any AI agent: **read → work → update → test → push**.
The system's whole promise — persistent project context across agents — holds
only if every session both starts AND ends with the files. Reading STATE.md
without rewriting it at the end breaks the chain for the next agent, which
might be a different tool, a different machine, or the same user next week.

## Session start (read)

1. **Sync.** `git pull` in the project repo (and in HQ if you have it
   locally). Report briefly if the pull isn't a fast-forward.
2. **Verify connections** the session will need, per HQ's `CONNECTIONS.md`.
   Troubleshoot failures now — a credential problem discovered mid-task is a
   session killer. If a fix needs something only the user can issue, ask
   immediately.
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

Do the session's work as normal. Two habits matter to the handoff:

- **Notice decisions as they happen.** "Chose X over Y because Z" and "tried
  A, failed because B" are the highest-value lines in the whole system —
  they're what stops the next agent from re-architecting or re-trying dead
  ends. Track them as you go; they're painful to reconstruct at the end.
- **Notice what GitHub can't see.** Unpushed branches, running local servers,
  half-applied migrations, files outside the repo. If it matters to the next
  session, it must be written into STATE.md, or it's invisible.

## Session end (update → test → push)

Update STATE.md **unprompted** whenever the session changed code, added or
removed a blocker, made a decision, or ends waiting on the user. This is part
of definition-of-done, not a favor.

1. **Rewrite** the project's `STATE.md` — rewrite, never append. Keep the
   format (Progress / Now / Next / Decisions / Open questions / Sync), target
   2KB. Fold new decisions into `decided/tried/rejected`; replace `## Now`;
   reorder `## Next` so item 1 is startable cold.
2. **Test the handoff.** Reread the file as if you were a fresh agent with no
   conversation history: could you start item 1 of `## Next` from the file
   alone? If not, it's not done — add the missing path, command, or context.
3. **Commit** as `state: <one-liner>` in the same batch as the session's code
   commits, and **push**. If the push fails, keep the local commit, set the
   Sync line to `last push: <date> | FAILED (<reason>)`, tell the user, and
   move on — never block on a push.
4. **Merge conflict on STATE.md?** Merge the Next lists, keep the newer Now
   and Progress, combine Decisions without duplicates, note the merge under
   `tried:`.

## Rules that keep the system honest

- Live status never goes in HQ — the map holds stable facts; the truth lives
  in each project's STATE.md.
- STATE.md is living decisions, not a changelog. A list of changed files
  helps nobody; the *why* does.
- Long-lived feature branches fork the handoff. Flag any branch that has
  outlived a couple of sessions; merge it promptly or declare it the only
  place its subsystem changes.
