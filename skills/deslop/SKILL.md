---
name: deslop
description: Remove AI writing patterns from prose. Use when writing, editing, or reviewing text to strip AI tells, slop, and formulaic patterns, or to humanize a draft. Applies to blog posts, scientific writing, memos, newsletters, and any substantial prose. Do not use for code or code comments, headline generation, or casual chat messages.
---

# Deslop

Remove formulaic AI tells while preserving the writer's specific voice.

## Modes

| Mode | Route when | Authority | Playbook |
| --- | --- | --- | --- |
| `edit` | The user asks to write, rewrite, revise, humanize, or deslop prose | Rewrite the text | [references/edit.md](references/edit.md) |
| `detect` | The user asks for an audit or findings without a rewrite | Report only | [references/detect.md](references/detect.md) |

Use `edit` by default for a change request. Honor an explicit `detect` request.
Do not infer authorship in either mode.

## Resources

Load a reference only when the work reaches it.

| Resource | Load when |
| --- | --- |
| [references/phrases.md](references/phrases.md) | You need the phrase-level tell catalog |
| [references/structures.md](references/structures.md) | You need the structural tell catalog |
| [references/tropes.md](references/tropes.md) | You need the trope catalog |
| [references/examples.md](references/examples.md) | You need a pattern-specific before-and-after example |

## Maintenance

- Last verified: 2026-11-17
- Target versions: voice skill, no library pins
- Owner: srdjan
- Re-verify when: new AI tells become common through model-version drift, or
  the core rule list grows past 10 items.
