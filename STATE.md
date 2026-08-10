# STATE - agent-handoff-skill (updated 2026-08-10 by codex @ maintainer)
## Progress
phase: live | percent: 100
done: public package with two validated skills, Codex UI metadata, five reusable templates, cross-platform setup, an explicit security model, private-by-default HQ guidance, and the README diagram
blocked: none
## Now
Public-readiness work is complete. The README now positions Agent Handoff as a Git-backed continuity layer, separates the public package from each user's private HQ and project state, and documents Claude Code, Codex, Cursor, and generic-agent use. Setup and ongoing handoffs explicitly minimize personal data and redact sensitive values.
## Next
1. Tag and publish the public-readiness release after the branch reaches main
2. Use the short problem/how-it-works/link reply when sharing the repository publicly
## Decisions
decided: keep one public distribution package and separate private user installations rather than maintaining two copies; generated HQ repositories default to private; the root STATE.md covers only this public package; hooks remain optional client adapters; public author credit and the personal workflow diagram remain intentionally
tried: both folders passed the skill-creator validator and fresh-agent setup/resume simulations; current-tree and Git-history secret-pattern scans passed; local Markdown links, skill frontmatter, diff whitespace, and image metadata passed; setup, documentation, and templates were reviewed as a first-time installation flow
rejected: bundling unrelated skills in the handoff package
rejected: rewriting published Git history for a non-secret repo-name mention - it would break existing clones and release ancestry
## Open questions
- none
## Sync
last push: 2026-07-22 | ok
