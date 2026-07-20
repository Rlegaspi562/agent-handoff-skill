# STATE - agent-handoff-skill (updated 2026-07-16 by claude-code @ cloud)
## Progress
phase: live | percent: 100
done: public template repo with two skills (agent-handoff-setup, agent-handoff), five templates, and the README diagram
blocked: none
## Now
Package trimmed: the writing-style skill and the unused draft diagram were removed from the public package. This file holds product state only.
## Next
1. Optional: description trigger checks on the two skills
2. Optional: tag a patch release so the release page matches the tree
## Decisions
decided: the public package carries only the handoff product (two skills + templates); repo STATE.md stays limited to product state; the writing-style skill lives outside this package
tried: full pre-ship scan (all files, both images, complete git history, releases): no credentials, private paths, or private-repo references found
rejected: bundling unrelated skills in the handoff package
## Open questions
- none
## Sync
last push: 2026-07-16 | ok
