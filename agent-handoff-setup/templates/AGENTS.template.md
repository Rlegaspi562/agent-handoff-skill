# Shared agent instructions

Applies to every registered project (see CONTEXT.md).

0. **Check required connections.** Before project work, verify the connections
   required for the task using `CONNECTIONS.md`. For hosted synchronization,
   verify GitHub. Ask the user if restoring access requires a credential or
   login they control.
1. **Session start:** read the project's `STATE.md` first. For cross-project
   questions ("what am I working on?"), read `CONTEXT.md` in this repo, then
   the relevant STATE.md files.
2. **Update STATE.md.** Update the file when a session changes code, blockers,
   decisions, or next actions, or stops pending user input. If you can edit
   the checkout, commit the update. If the remote allows writes, push it. If
   pushing fails, keep the local commit, set the Sync line to
   `last push: <date> | FAILED (<reason>)`, and create a second local state
   commit containing that failure record.
3. **Keep current status out of HQ.** Registry entries hold stable facts only,
   such as repository, local path, and a one-line description. Active
   branches, PRs, and blockers belong in each project's `STATE.md`.
4. **Record useful decisions.** Include rationale, failed attempts that should
   not be repeated, and enough context to continue. Do not use `STATE.md` as a
   file-change log.
5. **STATE.md format** (target <=2048 bytes, rewritten not appended): see
   `templates/STATE.template.md`: Progress, Now, Next, Decisions, Open
   questions, and Sync.
6. **Merge conflict on STATE.md:** merge the Next lists, keep the newer Now
   and Progress, combine Decisions without duplicates, and note the merge
   under Decisions/tried.
7. **Missing STATE.md:** inspect the repository README and recent Git history,
   then offer to create the file.
8. **Avoid conflicting branch state.** Long-lived branches can produce
   conflicting `STATE.md` versions. Do not change the same subsystem
   independently on both the feature and default branches.
