# Update an Existing Skill

## Objective

Align an existing skill with the architecture while preserving its intended
behavior. Do not redesign the skill contract here; a redesign changes trigger,
output, or authority and needs its own approval.

## 1. Reconstruct the Current Contract

Read the editable source, every routed owned file, metadata generator, variant
definition, catalog entry, tests, and install or package path. Do not trust a
generated `SKILL.md` as the source when a template or source manifest exists.

List:

- current trigger and non-trigger behavior,
- commands or modes,
- scripts and their callers,
- agents and their authority,
- editable sources and generated outputs,
- validation gates,
- known consumers and compatibility promises.

## 2. Compare by Responsibility

Use `architecture.md` to find concrete gaps. Common gaps are:

- a large entrypoint loads all playbooks for every request,
- command routes are implicit or duplicated,
- the same rule is edited in source and generated output,
- scripts perform model judgment or model prose performs exact parsing,
- agents have broad tools or vague return formats,
- required roles have no fallback on unsupported harnesses,
- tests assert prose instead of actions and artifacts,
- metadata, variants, or provider bundles drift from source.

Add commands, agents, scripts, or provider generation only when the skill needs
that responsibility. A reference implementation does not justify them by
itself.

## 3. Classify the Change

Classify each proposal as one of:

- structural and behavior-preserving,
- trigger or routing behavior change,
- output contract change,
- tool authority change,
- provider compatibility change.

Proceed directly only with structural, behavior-preserving changes that the
user requested. Ask before the other classes because they change external
behavior or authority.

## 4. Migrate One Boundary at a Time

Use this order:

1. establish the source-of-truth map,
2. add characterization or routing tests,
3. make the entrypoint a clear router,
4. move complete playbooks into references,
5. isolate deterministic work in scripts,
6. narrow or add agent contracts,
7. generate fallbacks and provider output,
8. regenerate metadata and variants,
9. remove outputs or copies made obsolete by this change.

Keep each step reviewable. Do not rewrite good domain guidance to match a
different voice. Preserve trigger phrases, output formats, and safety rules
unless the user approved their change.

## 5. Prove Parity

Run existing tests before and after when practical. Add tests for every moved
boundary. Verify:

- old trigger examples still route correctly,
- non-trigger examples remain excluded,
- every command loads the same or approved guidance,
- scripts preserve outputs and failure behavior,
- agents cannot write outside their boundary,
- generated files have no drift,
- install and package paths still discover the skill.

Forward-test one old request and one ambiguous adjacent request. If the result
changes, report it as a contract change instead of calling the update complete.

## Output Contract

Report the before and after source-of-truth map, behavior-preserving changes,
approved contract changes, checks run, and unresolved validation risk.

## Verification

Run the tests that covered the skill before the change. Then run the
repository gate. Confirm that every old trigger example still routes and that
non-trigger examples stay excluded. Confirm that generated files have no drift
and that install and package paths still discover the skill. Report a changed
result as a contract
change, not as a completed update.
