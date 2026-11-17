# Skill Architecture

Use this reference to select components and define their ownership. Include only
components that own a distinct responsibility.

## Architecture Levels

### Level 1: Focused skill

Use one `SKILL.md` and generated runtime metadata.

Choose this level when the workflow is linear, the instructions are short, and
one context can perform the work safely. Most skills should start here.

### Level 2: Routed skill

Keep a thin `SKILL.md` router. Put each distinct command or mode in one reference
file. Add shared references only for rules that several modes need.

Choose this level for a skill with several user intents. Choose it when
loading all guidance would waste context. Choose it when each mode has a
different output contract.

The router must define:

- the command or intent name,
- the trigger phrase or decision rule,
- the owning reference,
- the ambiguity rule,
- the default when no command is explicit.

Do not create a reference for every heading. A reference owns a complete
playbook, not a fragment that forces deep reference chains.

### Level 3: Operational skill

Add deterministic scripts and specialized agents to Level 2.

Choose a script when the work needs exact parsing, filesystem discovery,
validation, stable transforms, retries, or repeated command construction. The
script returns facts or performs a bounded operation. The model decides what
those facts mean.

Choose an agent when a role needs independent context, fresh review, different
tool authority, or an isolated write boundary. Do not use an agent as a longer
reference file.

Every agent definition needs:

1. a trigger and purpose,
2. required inputs,
3. allowed tools and write scope,
4. ordered checks or workflow,
5. a strict output contract,
6. stop and failure conditions,
7. a degraded inline path if the role is required on other harnesses.

### Level 4: Distributed skill

Add a source build and provider adapters to Level 3.

Choose this level only when one skill must ship to several harnesses with real
format differences. Keep a neutral source tree and transform only the provider
details:

```text
skill/
├── SKILL.src.md
├── references/
├── scripts/
└── agents/
        |
        v
provider transformers
        |
        v
generated runtime bundles
```

Provider adapters may change frontmatter fields, command prefixes, tool names,
agent file formats, hook manifests, and install paths. They must not fork the
domain workflow. Test at least one output from every affected provider.

## Source-of-Truth Map

Write this map before editing:

| Concern | Editable source | Derived output | Validator |
| --- | --- | --- | --- |
| Trigger contract | skill frontmatter | runtime metadata | frontmatter and metadata checks |
| Router | `SKILL.md` or source template | provider skill entrypoints | route coverage tests |
| Command | one reference playbook | optional pinned shortcut | command behavior tests |
| Deterministic action | script source | bundled script | unit and fixture tests |
| Specialist role | agent source | provider agent plus inline fallback | agent contract tests |
| Variant | template plus params | materialized `SKILL.md` | drift check |
| Distribution | neutral source tree | harness directories or archives | build and install smoke tests |

No row may have two editable sources. If users can edit both source and output,
drift is built into the architecture.

## Command Design

Use one parent skill with routed commands when the commands share vocabulary,
context, resources, and a user goal. Create separate skills when their trigger
surfaces, safety boundaries, or required expertise are independent.

Each command reference should contain:

- its objective and non-goals,
- prerequisites and required context,
- an ordered workflow,
- mutation and approval boundaries,
- an output contract,
- focused verification.

Store command metadata once when tooling needs descriptions, argument hints, or
generated shortcuts. Generate tables and counts from that source when drift has
caused real maintenance problems.

## Script and Tool Design

Keep side effects at the edge. Prefer pure parsing and planning functions with
explicit inputs and outputs. Wrap filesystem, process, browser, or network
access in small adapters.

Prefer Deno for structured tools and scripts. Use shell for small command
wrappers and process composition. Use another runtime only when repository
guidance requires it or a necessary dependency has no viable Deno or shell
path.

Scripts must:

- accept explicit paths and options,
- validate boundary inputs,
- avoid hidden global state,
- return structured output when another tool consumes the result,
- return a failure on partial or ambiguous work,
- avoid embedding repository or user secrets,
- include focused tests for success and failure paths.

Do not write a script for a classification or trade-off that a model can make
from the loaded evidence.

## Behavior Validation

Use three layers:

1. Structural checks verify files, frontmatter, links, metadata, and generated
   drift.
2. Deterministic tests verify scripts, transforms, provider output, and install
   layouts.
3. Behavior tests run realistic requests and assert the trace: required file
   reads, command routing, question order, tool calls, writes, scope, and final
   artifact state.

Use the trace and artifacts as evidence. Free-form model prose is not a stable
oracle. Record model and date when behavior tests depend on a live model.

## Reference Model: Impeccable

`pbakaus/impeccable` informed this architecture at commit
`32930818a109fafa87199babe92fa8e530cff5d3` from 2026-07-30. The levels and
validation layers above carry most of its transferable design. It also uses
one context script that loads durable project state once per session. Do not copy its
product-specific size into a smaller skill. Source:
<https://github.com/pbakaus/impeccable/tree/32930818a109fafa87199babe92fa8e530cff5d3>.
