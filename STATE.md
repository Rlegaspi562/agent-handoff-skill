# STATE - agent-handoff-skill (updated 2026-07-16 by claude-code @ cloud)
## Progress
phase: live | percent: 100
done: public template repo with two skills (agent-handoff-setup, agent-handoff), five templates, and the README diagram
blocked: none
## Now
v1.2 changes merged with Rumil's approval (2026-07-22): Orient step 0 in the daily loop, Orient + new-repo-registration rules in AGENTS.template.md, "HQ (entry point)" naming across README/skills/templates, and the setup skill now suggests `hq-entry-point` as the repo name. Origin: 2026-07-21 gap found live - an agent created a new repo from unregistered ground and skipped registration.
## Next
1. Tag a release so the release page matches the tree
2. Optional: description trigger checks on the two skills
## Decisions
decided: the public package carries only the handoff product (two skills + templates); repo STATE.md stays limited to product state; the writing-style skill lives outside this package
tried: full pre-ship scan (all files, both images, complete git history, releases): no credentials, private paths, or private-repo references found
rejected: bundling unrelated skills in the handoff package
## Open questions
- none
## Sync
last push: 2026-07-16 | ok
