# STATE - agent-handoff-skill (updated 2026-07-22 by codex @ main-pc)
## Progress
phase: live | percent: 100
done: public template repo with two skills (agent-handoff-setup, agent-handoff), five templates, and the README diagram
blocked: none
## Now
Current files use the concrete skill names only: `agent-handoff-setup` creates the system once, while `agent-handoff` handles a work session from context pickup through handoff. The misleading scheduled-sounding label was removed. Orient remains step 0 of `agent-handoff`.
## Next
1. Tag a release so the release page matches the merged tree
2. Optional: description trigger checks on the two skills
## Decisions
decided: the public package carries only the handoff product (two skills + templates); repo STATE.md stays limited to product state; the writing-style skill lives outside this package
tried: current-tree scan found no credentials, private paths, or private-repo references; old public history contains one private repo name but no path or secret, and history was not rewritten
rejected: bundling unrelated skills in the handoff package
rejected: rewriting published Git history for a non-secret repo-name mention - it would break existing clones and release ancestry
## Open questions
- none
## Sync
last push: 2026-07-22 | ok
