# STATE - agent-handoff-skill (updated 2026-07-22 by codex @ main-pc)
## Progress
phase: live | percent: 100
done: public template repo with two skills (agent-handoff-setup, agent-handoff), five templates, and the README diagram
blocked: none
## Now
Current files consistently describe the repo as the HQ entry point: the setup interview suggests `hq-entry-point`, its scaffold uses that directory name, and the templates contain no em dashes. Orient remains step 0 of the daily loop. The public package intentionally has no repo-local private HQ pointer files.
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
