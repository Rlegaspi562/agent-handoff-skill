# STATE - agent-handoff-skill (updated 2026-08-10 by codex @ maintainer)
## Progress
phase: live | percent: 100
done: public package with two validated skills, Codex UI metadata, five reusable templates, cross-platform setup, an explicit security model, private-by-default HQ guidance, the README diagram, and lightweight GIF and MP4 walkthroughs
blocked: none
## Now
Public-readiness release v1.2.0 is published from merged PR #8. The README positions Agent Handoff as a Git-backed continuity layer, separates the public package from each user's private HQ and project state, and documents Claude Code, Codex, Cursor, and generic-agent use. Setup and ongoing handoffs explicitly minimize personal data and redact sensitive values. The README now uses a small animated walkthrough linked to the full-resolution diagram, with a higher-quality MP4 available for social posts. GitHub recognizes Codex as a contributor.
## Next
1. Share the short problem/how-it-works/link reply in the relevant Reddit discussion
2. Publish the plain-language X launch post with the MP4 walkthrough
3. Collect real usage feedback before deciding whether to add optional client-specific enforcement hooks
## Decisions
decided: keep one public distribution package and separate private user installations rather than maintaining two copies; generated HQ repositories default to private; the root STATE.md covers only this public package; hooks remain optional client adapters; public author credit and the personal workflow diagram remain intentionally public; current public branches and tags use the maintainer's GitHub no-reply address
tried: both folders passed the skill-creator validator and fresh-agent setup/resume simulations; current-tree and Git-history secret-pattern scans passed; local Markdown links, skill frontmatter, diff whitespace, and image metadata passed; setup, documentation, and templates were reviewed as a first-time installation flow
rejected: bundling unrelated skills in the handoff package
rejected: rewriting published Git history for a non-secret repo-name mention - it would break existing clones and release ancestry
## Open questions
- none
## Sync
last push: 2026-08-10 | ok
