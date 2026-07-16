# Global agent contract

Applies to every registered project (see CONTEXT.md).

0. **Connections bootstrap.** Before project work, verify the connections this
   session will need — GitHub always; anything else as the task demands.
   Verify commands and fixes live in `CONNECTIONS.md`. Troubleshoot a broken
   connection FIRST; if the fix needs a credential only the human can issue,
   ask right away rather than discovering it mid-task.
1. **Session start:** read the project's `STATE.md` first. For cross-project
   questions ("what am I working on?"), read `CONTEXT.md` in this repo, then
   the relevant STATE.md files.
2. **STATE.md is part of definition-of-done.** Any session that changes code,
   adds/removes a blocker, makes a decision, or ends waiting on the human MUST
   update `STATE.md` in the same commit batch — without being asked. Rewrite
   it (format below), commit `state: <one-liner>`, push. If push fails, keep
   the local commit and set the Sync line to
   `last push: <date> | FAILED (<reason>)`. Never block on push.
3. **Never put live status in HQ.** Registry entries hold stable facts only
   (repo, local path, one-line description). Live status — active branches,
   PRs, blockers — lives in each repo's STATE.md.
4. **STATE.md is living decisions, not a changelog.** Prefer "we chose X over
   Y because Z" and "tried/rejected A because B" over a list of files changed.
   Keep enough progress detail that a new agent can continue without
   re-architecting.
5. **STATE.md format** (target <=2048 bytes, rewritten not appended): see
   `templates/STATE.template.md` — Progress / Now / Next / Decisions /
   Open questions / Sync.
6. **Merge conflict on STATE.md:** merge the Next lists, keep the newer Now
   and Progress, combine Decisions without duplicates, and note the merge
   under Decisions/tried.
7. **Missing STATE.md:** fall back to `git log --oneline -10` + this file,
   then offer to create one.
8. **Long-lived feature branches fork the handoff — avoid them.** A branch
   that outlives a couple of sessions grows its own STATE.md truth while the
   default branch keeps moving. Either merge promptly, or make the branch the
   ONLY place its subsystem changes until it merges.
