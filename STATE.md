# STATE - agent-handoff-skill (updated 2026-07-16 by claude-code @ cloud)
## Progress
phase: live | percent: 100
done: public template repo with two skills (agent-handoff-setup, agent-handoff), five templates, and the README diagram
blocked: none
## Now
Branch feat/orient-and-new-repo-rule (PR pending Rumil's review) adds the Orient step 0 to the daily loop, an Orient + new-repo-registration rule to AGENTS.template.md, and "HQ (entry point)" naming across README, setup skill, and templates. Origin: 2026-07-21 gap found live - an agent created a new repo from unregistered ground and skipped registration; neither skill covered "new project" or "locate yourself first".
## Next
1. Rumil reviews and merges the PR, then tag a release
2. Optional: description trigger checks on the two skills
## Decisions
decided: the public package carries only the handoff product (two skills + templates); repo STATE.md stays limited to product state; the writing-style skill lives outside this package
tried: full pre-ship scan (all files, both images, complete git history, releases): no credentials, private paths, or private-repo references found
rejected: bundling unrelated skills in the handoff package
## Open questions
- none
## Sync
last push: 2026-07-16 | ok
