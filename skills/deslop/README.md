# deslop

A Claude skill for removing AI writing patterns from prose.

## What it does

When you write, draft, edit, or review text, `deslop` finds and removes predictable AI tells: formulaic sentence structures, filler phrases, false agency, dramatic fragmentation, vague declaratives, and dozens of other patterns.

The rules apply to any prose. The examples lean toward scientific writing and technical blog posts. In scientific text, the skill keeps field conventions such as passive voice in methods sections and domain-specific terminology.

## Installation

See the [repository README](../../README.md) for installation and checks.

## How to use it

After installation, talk to Claude as you normally do. The skill triggers automatically when you:

- Ask Claude to write prose, such as a blog post, essay, article, memo, or newsletter, that sounds natural instead of AI-generated
- Ask Claude to "deslop", "de-AI" or "make it sound human"
- Ask Claude to check for "slop" or AI patterns

You can also reference the skill directly:

- "Review this draft using the deslop checklist"
- "Score this text on the deslop rubric"
- "Rewrite this paragraph to pass the deslop quick checks"

## Scoring rubric

The skill includes a 1-10 scoring rubric across five dimensions:

| Dimension    | Question                               |
| ------------ | -------------------------------------- |
| Directness   | Statements or announcements?           |
| Rhythm       | Varied or metronomic?                  |
| Trust        | Respects reader intelligence?          |
| Authenticity | Sounds like a specific human wrote it? |
| Density      | Anything cuttable?                     |

Below 35/50: revise.

## Skill structure

```
deslop/
├── SKILL.md              # Router for edit and detect modes
├── README.md             # This file
├── LICENSE               # MIT license
├── agents/
│   └── openai.yaml       # OpenAI interface metadata
└── references/
    ├── edit.md           # Rewrite playbook and scoring rubric
    ├── detect.md         # Findings without a rewrite
    ├── phrases.md        # Phrases to remove or replace
    ├── structures.md     # Structural patterns to avoid
    ├── tropes.md         # Full catalog of AI writing tropes
    └── examples.md       # Before/after transformations
```

## Acknowledgments

Parts of this skill adapt material from two open sources:

- The AI writing tropes catalog from [tropes.fyi](https://tropes.fyi/) by [Ossama Hassanein](https://ossama.is). The `references/tropes.md` file is adapted from this source, and its trope patterns appear throughout the other reference files.
- stop-slop from [github.com/hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop) by [Hardik Pandya](https://hvpandya.com). The phrase lists, structural patterns, before/after examples, scoring rubric, and quick checks draw from this project.

## License

MIT
