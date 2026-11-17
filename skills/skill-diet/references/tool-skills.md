# Skills for tools

## Objective

Keep tool guidance accurate while reducing copied reference material.

## Inventory and drift

List public operations from the tool's current help or source.
Find every documentation copy, installed skill, embedded prompt, and generated reference.
Prove each rejected name, ignored parameter, missing operation, or incorrect behavior through execution or a source location.
A matching operation name does not prove parameter behavior.
Measure help size and factual overlap with the skill.

## Usage evidence

When authorized logs exist, count operations, errors, and sessions that read the skill.
Deduplicate repeated call identifiers across resumed and forked sessions.
Inspect nested calls inside tool results.
Otherwise, report that usage evidence is unavailable.
Select essential examples from task requirements without inventing frequency claims.

Keep three parts in the tool guidance:

- Common operations with one complete call each.
- Difficult argument shapes with one working example each.
- Remaining public operation names, grouped for discovery.

Use [formats.md](formats.md) for examples in the actual call syntax.

## Help and errors

Replace skill reference text with tool help only when that help covers the relevant decision.
Check that unknown operations suggest valid alternatives.
Check that unknown parameters fail visibly.
Check that common errors explain a corrective action.
If those checks fail, retain the necessary guidance until the tool improves.

If the user authorizes tool changes, fix errors and checks before relying on them.
Preserve accepted fields and their validation when reducing tool schemas.
Keep rules in tool descriptions only when the rules must prevent the first call.
Pin such descriptions when their exact contents form a compatibility promise.

## Verification

Check that every documented name, parameter, and value resolves.
Check that the discovery index names every public operation.
Keep a coverage check for recurring drift in a tool the user controls.
Run all skill versions against the same tool version and help behavior.
Include a no-skill version with access to the tool's own help.
For native tools, expose the actual schema or a stub without side effects.

For CLI evaluation, run `scripts/observe.mjs shim <tool> <bin-dir>` through Deno.
Use a private directory for the shim and call log.
Follow the printed command to run the evaluator with the shim first on `PATH`.
Run `scripts/observe.mjs --summary <log>` through Deno for counts by version.
The logger covers CLI subprocesses only.
Use recorded agent calls for MCP tools, native tools, APIs, and SDKs.

## Output Contract

Report proven drift, operation coverage, usage evidence, valid first calls, incorrect calls, help volume, and required tool changes.
Do not claim measured operation frequencies without logs.
