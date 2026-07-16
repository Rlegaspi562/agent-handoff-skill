---
name: anti-ai-slop
description: Edits public or user-facing prose to remove AI-sounding language while preserving meaning, voice, structure, and technical accuracy. Use when asked to rewrite a README, documentation, script, post, email, brief, or product copy; remove AI slop; make writing sound human; enforce a no-em-dash rule; or audit generated prose. Do not use for raw code or command output unless the user asks for comments or surrounding copy to be edited.
---

# Anti AI Slop

Write like a person who understands the subject and has something specific to
say. Prefer plain facts, concrete instructions, and honest limits.

## Defaults

- Use direct, plain language.
- Keep sentences easy to read without making every line a slogan.
- Use concrete nouns, commands, files, costs, and outcomes.
- State conditions and limitations where they matter.
- Preserve the author's meaning and level of confidence.
- Preserve technical names, commands, paths, URLs, code, and frontmatter.
- Do not use em dashes.

## Pass 1: remove obvious AI copy

Remove or rewrite:

- Generic openings such as "Certainly," "Absolutely," "Great question," and
  "Let's dive in."
- Filler endings such as "Hope this helps," "Happy to help," and "Let me know
  if you need anything else."
- Generic AI vocabulary: unlock, leverage, utilize, delve, robust, seamless,
  elevate, supercharge, cutting-edge, revolutionary, game-changer.
- Empty praise: powerful, transformative, next-level, best-in-class,
  world-class.
- Unsupported universal claims using words such as everyone, always, never,
  any, or guaranteed.
- Competitor claims that were not checked.
- The word "hype" in public copy. Name the specific noise, claim, or trend
  instead.

Replace every em dash in prose with a period, comma, colon, parentheses, or a
rewritten sentence.

## Pass 2: remove structural slop

Rewrite passages that contain:

- Several polished but abstract sentences in a row.
- Repeated "this is not X, it is Y" constructions.
- Short slogan fragments that replace an explanation.
- Neat groups of three that add rhythm but not information.
- Vague metaphors such as glue, magic, brain, engine, or operating system when
  the text does not explain the mechanism.
- Claims that a tool acts automatically when it actually depends on access,
  synchronization, configuration, or user behavior.
- Dramatic language such as "session killer," "the whole promise," or "the
  highest-value part."
- Corporate headings such as "Key takeaways," "What's in the box," or
  "Unlocking value" when a literal heading would be clearer.
- Repetition of the same point in the heading, paragraph, bullets, and closing.

Do not remove personality. Keep useful opinions, humor, cultural references,
and conversational grammar when they sound like the author.

## Accuracy pass

Before finalizing:

1. Separate observed facts from assumptions and recommendations.
2. Check whether each broad claim has stated requirements.
3. Do not describe saved files as automatic model memory.
4. Do not imply that read access includes commit or push permission.
5. Do not imply that committed work is available elsewhere until it has been
   pushed and fetched or pulled.
6. Do not claim a named guide, source, test, or integration was used unless it
   was actually checked.
7. Keep privacy-sensitive facts out of public copy.

## Editing method

1. Read the full document before rewriting individual lines.
2. Identify the audience and the action the document should help them take.
3. Delete sentences that do not change meaning or action.
4. Rewrite the remaining copy in the author's voice.
5. Preserve code blocks, commands, links, identifiers, and file structure.
6. Run a final scan for em dashes, banned words, overclaims, and repeated
   sentence patterns.
7. Read the result aloud. Fix stiff cadence, stacked fragments, and sentences
   that sound written for a slide instead of a person.

## Repository workflow

When editing a repository:

1. Read its instructions and `STATE.md` first.
2. Audit all public Markdown, not only the README.
3. Use text search to verify that no em dashes or banned words remain.
   Exclude this skill's own rule list when counting banned-word matches.
4. Validate links, skill frontmatter, templates, and formatting after edits.
5. Update `STATE.md` with the decision and next action.
6. Commit and push on a branch when access permits.

## Output

If file-editing tools are available, edit the files directly. Return a short
summary of what changed and what was verified.

If the user asks for copy only, return the finished copy first. Do not surround
it with a long explanation of the editing process.
