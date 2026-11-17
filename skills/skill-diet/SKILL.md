---
name: skill-diet
description: Keep agent skills lean and correct. Use before editing a skill, adding a lesson, updating documented tool behavior, or reducing skill context with before/after evaluations. Do not use for creating a skill or redesigning its architecture (use create-skill), ordinary prose editing, or code cleanup.
---

# Skill Diet

Put each fact at the lowest level that reaches the agent before the agent needs it.

| Level | Content | Read when |
| --- | --- | --- |
| Description | Triggers and exclusions | Skill discovery |
| `SKILL.md` | Rules every task needs | Skill invocation |
| References | Guidance for specific cases | The router selects that case |
| Tool help | Current names, fields, values, and examples | The agent selects an operation |
| Tool replies and checks | Corrections and mechanical constraints | The agent calls the tool |

## Editing a skill

Stop at the first step that handles the change.

1. Fix mechanical mistakes in the tool's errors, checks, or tests.
2. If a fresh session already follows the proposed rule, add nothing.
3. Edit the existing rule instead of appending another copy.
4. Place the rule at the lowest suitable level.
5. Write the rule; put the incident and rationale in the commit message.

When code changes documented names or behavior, update the skill in the same change.
Record the entrypoint's byte size before and after in the commit message.
Offset additions with cuts where the cuts preserve behavior.
When growth exceeds 10% since the last diet, or rules repeat, use the full diet workflow.

This threshold is an upstream maintenance rule, not a measured performance claim.
Rerun the case that prompted the edit in a fresh session.
Run the applicable repository checks.

Do not run evaluation tasks against real accounts or production data.
Use disposable fixtures and isolated agent configuration.
Keep raw logs and credentials outside committed artifacts.

## Routes and tools

For a full reduction or accuracy review, read [references/diet.md](references/diet.md).
For tool-specific checks, read [references/tool-skills.md](references/tool-skills.md).
For command notation, read [references/formats.md](references/formats.md).
For before/after evaluation, read [references/eval.md](references/eval.md).
For the agent adapter contract, read [references/adapter.md](references/adapter.md).

Replace `/absolute/path/to/skill-diet` with the absolute directory that contains
this loaded `SKILL.md`. Write that path into the command. Do not set a shell
variable for the path. A command allowlist can block a command that sets and
uses a variable.
Run scripts rather than loading their source or raw evaluation logs into context.

```bash
deno run -A /absolute/path/to/skill-diet/scripts/eval.mjs check <skill-dir>
deno run -A /absolute/path/to/skill-diet/scripts/eval.mjs --help
```

`scripts/eval.mjs` owns calibration, execution, scoring, and link checks.
`scripts/observe.mjs` logs CLI calls and summarizes their outcomes.
Both scripts use Deno's compatibility APIs for Node built-ins.
No package installation is required.
The checker reports bytes, not model tokens.
The adapter reports measured model tokens.

For provenance and local script changes, read [UPSTREAM.md](UPSTREAM.md).
The upstream MIT notice is in [LICENSE](LICENSE).

## Maintenance

- Last verified: 2026-10-27
- Target versions: Deno 2.9.8 and the upstream adapter result contract
- Owner: srdjan
- Re-verify when: the evaluation contract changes.
