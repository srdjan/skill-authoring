# Create or Extract a Skill

## Objective

Build a new skill, or extract a reusable skill from a repository, workflow,
command set, or repeated task. Do not use this playbook to change an existing
skill's behavior; that is `update`.

## 1. Establish the Boundary

Collect or infer:

- two to four requests that must trigger the skill,
- two requests that must route elsewhere,
- the artifact or outcome the skill must produce,
- read-only and write-capable modes,
- required approvals,
- supported runtimes or harnesses.

Search the current catalog before naming the skill. Extend an existing skill
when the new requests share its domain and workflow. Prefer a short verb-led
kebab-case name under 64 characters.

## 2. Inspect the Reference Material

When extracting from another repository, inspect the editable sources, build
logic, generated outputs, tests, install paths, and project guidance. Separate
the domain-specific content from the reusable architecture.

Record the upstream URL, inspected commit, license, and files that informed the
design. Summarize patterns in your own words. Do not import generated output or
product-specific complexity that the new skill does not need.

## 3. Select the Architecture

Read `architecture.md` and choose the lowest sufficient level.

Start with this structure:

```text
skills/<skill-name>/
├── SKILL.md
└── agents/
    └── openai.yaml
```

Add only justified resources:

```text
├── references/     # complete on-demand playbooks or deep domain references
├── scripts/        # deterministic operations with focused tests
├── assets/         # files copied into user output, not instructions
├── agents/         # runtime metadata and supported specialist roles
├── SKILL.template.md
└── params/         # declared materialized variants only
```

## 4. Write the Router

Write frontmatter first. The description must state:

1. what the skill does,
2. concrete requests or contexts that trigger it,
3. a `Do not use for...` clause that separates adjacent skills.

Keep the body imperative. Put universal rules and the route table in
`SKILL.md`. Put task-specific workflows in references. Mention every owned
resource from the entrypoint so it can be discovered and validated.

## 5. Add Operational Parts

For every proposed script, state the nondeterminism or repetition it removes.
For every proposed agent, state why separate context or authority improves the
result. Remove any component without a distinct answer.

Use Deno for structured tools and scripts. Use shell for thin command wrappers
and process composition. Add another runtime only when repository guidance or a
required dependency makes it necessary.

If the skill supports commands, give each command one owner and one output
contract. If the skill supports several providers, keep provider syntax in
adapters and shared behavior in one neutral source.

## 6. Generate and Validate

Use the repository's initializer when one exists. Generate runtime metadata and
variants through their source tooling. Add the skill to the canonical catalog.

Run focused checks while iterating. Finish with the full repository gate. For a
routed or operational skill, forward-test at least one natural-language request
that does not name the command. This proves trigger and routing behavior rather
than command parsing alone.

### Repository Checks

Use the target repository's catalog, metadata generators, and validation commands when they exist.
Do not invent generators or registry files for a repository that does not need them.
In this standalone repository, run `deno task check` from the repository root.
This command checks bundled Markdown links and entrypoint sizes.
It does not test live model behavior.

## Output Contract

Report:

- the skill boundary and non-trigger boundary,
- the selected architecture level,
- the source-of-truth map,
- files added or generated,
- exact checks and forward-tests run,
- any provider or behavior validation not run.

## Verification

Run the repository's focused validators, then its full gate. Confirm that every
owned file is routed from the router, that generated metadata has no drift, and
that the forward-test routed to the intended playbook. Report any check that
could not run and why.
