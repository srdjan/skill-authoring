# Audit a Skill Architecture

## Objective

Report on a skill's architecture without changing it. This playbook is
report-only. Do not edit files, and do not run a validator that generates or
fixes them.

## Evidence Pass

Inspect repository guidance, the canonical catalog, the editable skill source,
routed references, scripts, assets, agent definitions, generators, variants,
tests, and install or package code. Follow references from the entrypoint. Avoid
broad scans of unrelated product code.

Run non-mutating validators when they are fast and repository-approved. If a
validator generates or fixes files, do not run it in an audit.

## Checks

Evaluate:

1. Boundary: trigger and non-trigger examples are explicit and do not
   overlap another skill without a routing rule.
2. Progressive disclosure: the entrypoint contains universal instructions
   and routes complete task playbooks on demand.
3. Command ownership: each command has one route, one purpose, and one
   output contract.
4. Determinism: scripts own exact operations while the model owns judgment.
5. Agent authority: each agent has justified isolation, least privilege,
   explicit inputs, outputs, and stop conditions.
6. Source authority: every rule has one editable source and all derived
   files are generated or checked for drift.
7. Behavior proof: tests cover trigger, routing, action order, boundaries,
   failure paths, artifacts, and provider output where applicable.
8. Maintenance: catalog, metadata, freshness anchors, install paths, and
   full gates match repository conventions.

Verify every finding against a concrete file, route, or failing check. Do not
report missing advanced architecture as a defect unless a real use case needs
it.

## Output Contract

```text
## Verdict
Architecture level: <1-4>
Status: aligned | partially aligned | misaligned

## Findings
P0-P3 | <path> | <verified gap> | <user or maintenance impact>

## Source-of-truth map
<concern -> editable source -> generated outputs -> validator>

## Migration plan
1. <small behavior-preserving unit> -> verify: <exact check>

## Already correct
<important architecture that should not be changed>

## Validation limits
<checks not run and why>
```

Order the migration plan by dependency. Put characterization tests before moved
behavior and source authority before generated output cleanup.

## Verification

Confirm that every finding cites a concrete file, route, or failing check.
Reject a finding that rests on missing advanced architecture the skill has no
use case for. Confirm the working tree is unchanged: an audit that wrote a file
is a failed audit. List the checks not run under Validation limits.
