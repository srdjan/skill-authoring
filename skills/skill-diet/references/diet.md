# Full diet

## Objective

Reduce a skill's loaded context or correct drift without losing required behavior.

## 1. Baseline

Copy the complete skill into the evaluation's `before` directory.
Record description size, entrypoint size, reference sizes, and typical loaded context.
Use actual usage reports for model token counts.
When token counts are unavailable, report bytes and the measurement limit.

Find callers, linked skills, generated copies, embedded prompts, tests, and installed names.
Confirm that the runtime loads the intended copy.
Check the runtime's current read limit before moving content into large references.
Keep guidance for other supported users even when local sessions do not use it.

Read session logs only within the user's authorized scope.
Keep extracted reports limited to counts and anonymous findings.

## 2. Tool accuracy

If the skill teaches a tool, complete [tool-skills.md](tool-skills.md) before rewriting.

## 3. Evaluation and placement

Write [evaluation tasks](eval.md) while only the original version exists.
Include the user's recent case and each risky boundary.
Place each fact according to the levels in the entrypoint.
Keep frequently required guidance in the entrypoint.
Route occasional guidance to references with explicit read conditions.
Run scripts and copy assets instead of reading their source into context.

If only explicit invocation is intended, check the host's current metadata contract.
Set invocation policy through the metadata's source or generator.
Never edit generated runtime metadata directly.

## 4. Rewrite

Remove common knowledge only when the no-skill evaluation supports removal.
Move human rationale and measurements into provenance or the commit message.
Replace repeated examples with their governing rule when that rule preserves behavior.
Keep safety constraints for writes, data transfer, credentials, and paid operations explicit.
Do not remove a necessary rule merely to meet a size target.

## 5. Verify

Run the evaluation and inspect every failure.
Use a fresh reviewer to check every original rule against the revised skill.
Record each retained, relocated, or removed rule and its evidence.
For an uncovered removal, add a case and run the revised skill three times.
Restore the rule unless every run succeeds.
Give the reviewer anonymous outputs when quality requires model judgment.

Require a complete scoring matrix and a successful scorer exit.
Require fewer measured tokens per run or a demonstrated correction of drift.
If the evaluation is unavailable, report the rewrite as unvalidated.
Do not claim behavior parity from structural checks alone.

## Output Contract

Report sizes by level, measured tokens per run, results by task, moved rules, removed rules, and required tool changes.
Name incomplete checks and the exact behavior they leave uncertain.

## Verification

Run the link checker, the repository gates, and [the complete evaluation](eval.md).
Keep the original skill available until the revised skill passes.
