---
name: create-skill
description: Create, extract, audit, or modernize agent skills. Use when a repeated workflow or reference repository must become a skill, or a skill's architecture needs review or update. Do not use for third-party skill installation or discovery, ordinary documentation, or product code that does not change a skill.
---

# Create Skill

Create the smallest skill architecture that handles the real use cases. Keep a
simple skill simple. Add commands, scripts, agents, or provider generation only
when each part has a distinct job and a testable contract.

For edits to an existing skill, read [skill-diet](../skill-diet/SKILL.md), section "Editing a skill".
Keep architecture work in this skill; use the diet workflow for measured reduction.

## Inputs to Establish

Establish only the inputs needed by the selected mode:

- Read the repository guidance that governs the requested skill surface. Do not
  load unrelated docs.
- Search for overlapping skills when creating a skill or changing its trigger
  boundary. Extend an existing skill when its domain and workflow overlap.
- Locate the editable source. Regenerate `SKILL.md` when a template, generator,
  or source directory owns it. Never hand-edit a generated skill or runtime bundle.
- Capture trigger and non-trigger examples when routing behavior can change.
  Infer them from the request and repository when possible. Ask only when a
  missing answer would change the skill boundary.
- Read [references/architecture.md](references/architecture.md) and the selected
  command playbook. Use the lowest architecture level that satisfies the
  examples.

## Commands

Choose one mode from the request. Load only its playbook.

| Command | Use | Playbook |
| --- | --- | --- |
| `create` | Create a new skill or extract one from a workflow, repository, or repeated task | [references/create.md](references/create.md) |
| `update` | Align an existing skill with the architecture without changing its intended behavior | [references/update.md](references/update.md) |
| `audit` | Report architecture gaps and a source-backed migration plan without editing | [references/audit.md](references/audit.md) |

Natural requests do not need the command word. Route "turn this into a skill"
to `create`, "bring this skill up to date" to `update`, and "review this skill
architecture" to `audit`. Ask once if both `update` and behavior redesign fit,
because an update preserves the skill contract while a redesign changes it.

## Architecture Invariants

- Treat the frontmatter description as a public trigger API. State what the
  skill does, when it triggers, and when it must not trigger.
- Keep `SKILL.md` as the discoverable contract and router. Move detailed or
  task-specific playbooks into references that load only when routed.
- Use scripts for deterministic facts, parsing, validation, transforms, and
  repeated operations. Keep judgment, drafting, and trade-off analysis in the
  model instructions.
- Add an agent only for a role that benefits from separate context or separate
  tool authority. Give it a narrow input contract, output contract, tool set,
  stop condition, and write boundary.
- Provide an inline fallback when a required workflow must work in a harness
  without supporting agents. Generate the fallback from the agent source when
  a build system exists.
- Keep one editable source for every rule. Generate runtime metadata, variants,
  provider bundles, command indexes, and fallback copies from that source.
- Validate observable behavior. Test routing, required reads, tool-call order,
  writes, boundaries, and outputs. Do not accept a fluent final answer as proof.
- Preserve unrelated files and local changes. Ask before changing an existing
  skill's external behavior, trigger boundary, output contract, or data
  semantics.
- Write skill prose in ASD-STE100. Keep each sentence at 25 words or fewer and
  each paragraph at six sentences or fewer. Use a list for three or more steps
  or conditions.

## Definition of Done

- The trigger contract distinguishes matching and non-matching requests.
- The source map names editable sources, generated outputs, install targets,
  and validation gates.
- Each concern has one owner. Every owned resource has an entrypoint route.
- Existing repository tooling produced any generated metadata and variants.
- Focused validators and the full repository gate pass.
- Non-trivial routing, scripts, or agents have a forward test. The evaluator
  receives the skill and request, not the intended answer.
- The final report explains what changed, why each component exists, and the
  exact verification commands.

## Repository Profile

In this standalone repository:

- Keep each skill in `skills/<name>/`.
- Maintain frontmatter and `agents/openai.yaml` together.
- Use unprefixed skill names in cross-references and default prompts.
- Keep each resource reachable from its `SKILL.md` router.
- Preserve license notices when copying third-party resources.
- Run `deno task check` before completion.

When the target repository owns metadata generators, use those generators instead of editing generated files.

## Maintenance

- Last verified: 2026-11-17
- Target versions: Agent Skills SKILL.md format and the bundled Deno link checker
- Owner: srdjan
- Re-verify when: skill discovery, agent metadata, provider generation, or repository validation rules change.
