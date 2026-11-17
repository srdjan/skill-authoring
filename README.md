# Skill Authoring

Three agent skills, extracted from Gotai into a standalone repository.

| Skill | Purpose | Entrypoint |
| --- | --- | --- |
| `create-skill` | Create, extract, audit, or update agent skills | [SKILL.md](skills/create-skill/SKILL.md) |
| `deslop` | Remove formulaic AI writing patterns from prose | [SKILL.md](skills/deslop/SKILL.md) |
| `skill-diet` | Keep skills lean and evaluate changes | [SKILL.md](skills/skill-diet/SKILL.md) |

## Installation

Copy the three directories under `skills/` into the skills directory supported by your agent.
Keep each complete directory, including its references, scripts, metadata, and license notices.
The agent must support the `SKILL.md` format.
This repository includes OpenAI interface metadata in each `agents/openai.yaml` file.
It does not require the Gotai plugin or the original repository tooling.

## Use

Name the skill in a request, or let an agent select the skill from its description.

```text
Use create-skill to extract this workflow into a reusable skill.
Use deslop to revise this draft while preserving my voice.
Use skill-diet to review this skill for repeated instructions.
```

`create-skill` provides create, update, and audit playbooks.
`deslop` provides edit and detect modes.
`skill-diet` includes evaluation tools and a contract for an agent adapter.
A live evaluation requires an adapter for your agent CLI.
The repository does not include an adapter or credentials.

## Checks

Deno is required only for the scripts and checks.
The extraction checks ran with Deno 2.9.8.
No package installation is required.

From the repository root:

```sh
deno task check
```

This command reports each entrypoint's byte size and checks local Markdown links and heading anchors.
It does not prove live agent behavior or model quality.

The evaluation tool also provides command help:

```sh
deno run --no-config --allow-read skills/skill-diet/scripts/eval.mjs --help
```

## Maintenance

Skill entrypoints, references, scripts, and interface metadata are editable sources.
This repository has no metadata generator.
When a skill name changes, update its frontmatter, references, and default prompt together.
Keep evaluation fixtures, logs, and temporary adapters in the ignored `demos/` directory.

## Source and licenses

Extracted on 2026-11-17 from `srdjan/_skills` at commit `54a59379b09037b2e439dcb212bb41c9f12826fa`.
The extraction changes namespace references and repository instructions.
The evaluation scripts retain their original contents.

The [root MIT license](LICENSE) covers the Gotai material.
`deslop` retains its [MIT license](skills/deslop/LICENSE), copyright Stephen D. Turner.
Its [README](skills/deslop/README.md#acknowledgments) preserves upstream acknowledgments.
`skill-diet` retains its [MIT license](skills/skill-diet/LICENSE) and [upstream provenance](skills/skill-diet/UPSTREAM.md).
