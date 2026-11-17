# Before/after evaluation

## Objective

Compare the original skill, revised skill, and no skill under the same conditions.

## Tasks and fixtures

Write tasks before editing the original skill.
Use real requests when authorized session evidence is available.
Include the user's named case, each routed workflow, each prohibition, and each risky operation.
Use disposable fixtures for operations that change state.
For real accounts, evaluate the proposed action without executing it.

Use this layout:

```text
<dir>/tasks.json
<dir>/adapter
<dir>/sk/before/<skill>/
<dir>/sk/after/<skill>/
```

The `none` version has no skill directory.
Each task has an identifier, request, and assertions over its result or final state.

```json
[{"id":"case-one","prompt":"Use the deploy skill to prepare a deployment.","must":["plan"],"must_not":["deploy --production"],"setup":"touch fixture","check":"test -f fixture"}]
```

`must` matches the reply; `must_not` matches executable lines in fenced code blocks.
`check` evaluates state after the adapter exits.
Text matching alone does not prove the agent avoided a prohibited tool call.
Use a checker over the recorded calls when a task requires that guarantee.

## Execution

Write or reuse [the adapter](adapter.md) for the current agent CLI.
Use the same model and fresh sessions for every version.
Keep adapters, raw logs, fixtures, and evaluation results in an ignored local directory.
In this repository, use `demos/skill-diet/`.

First run two tasks to check the full pipeline.
Then change only the selected task set to run the full evaluation.
Run each task three times per version.
Use the same version and run arguments for execution and scoring.

```bash
deno run -A /absolute/path/to/skill-diet/scripts/eval.mjs --help
deno run -A /absolute/path/to/skill-diet/scripts/eval.mjs calibrate <dir> --model <model>
deno run -A /absolute/path/to/skill-diet/scripts/eval.mjs run <dir> --tasks case-one,case-two --model <model>
deno run -A /absolute/path/to/skill-diet/scripts/eval.mjs score <dir> --tasks case-one,case-two
deno run -A /absolute/path/to/skill-diet/scripts/eval.mjs run <dir> --model <model>
deno run -A /absolute/path/to/skill-diet/scripts/eval.mjs score <dir> --detail
```

Execution calibrates the adapter again before starting unfinished runs.
Completed runs remain available for resumption.
If a task changes, remove its old runs and rerun every version.
Never reuse results from an earlier task definition.

## Verification

Read every failing result before changing the skill or assertions.
If an assertion rejects a valid answer, give an independent reviewer only the task and answer.
Change the assertion only after that review confirms the answer satisfies the task.
Rerun changed tasks in every version.
For quality judgments, use the skill's checker and anonymous pairs in random order.

A `MISS` means the original passed every run while the revision passed none.
A `WORSE` result means the observed success-rate reduction exceeds the scorer's statistical threshold.
These labels describe the sampled tasks; they do not establish general behavior parity.
Run the suggested additional repetitions before accepting a disputed result.
Move missing guidance to a level the agent reads before adding more prose.

## Output Contract

Report the model, date, task coverage, complete result matrix, tokens, tool calls, failures, and remaining limits.
A successful synthetic adapter test proves evaluation mechanics only.
