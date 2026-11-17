# Agent adapter

## Objective

Run one isolated agent session and report its measured usage and calls.

## Invocation

Create an executable at `<dir>/adapter` using the current agent CLI's help.
The evaluator calls the adapter with four arguments:

```text
<dir>/adapter <skill-dir> <prompt> <out-dir> <work-dir>
```

An empty skill directory selects the no-skill version.
Use the model from `EVAL_MODEL` when the evaluator supplies it.
Work in the supplied work directory.
Expose exactly the supplied skill, or no skills for an empty argument.
Hide installed skills, plugins, memory, and unrelated instruction files through disposable configuration.

Preserve the user's actual configuration and authentication files.
Keep all temporary authentication material private and outside committed files.

Allow file reads and shell commands without interactive prompts inside the disposable fixture.
Preserve the evaluator's environment, including `PATH` and `OBSERVE_*`.
Runs can overlap; never share mutable files between runs.

## Output Contract

Write `<out-dir>/result.json` and retain raw agent output in the output directory.

```json
{"answer":"final reply","tokens":{"input":10,"output":5,"cacheRead":0,"cacheWrite":0},"turns":1,"calls":[{"name":"read","path":"/absolute/skill/SKILL.md"},{"name":"shell","command":"example"}]}
```

Report usage from the agent's actual output.
The numbers above illustrate the schema; they are not measurements.
Exclude cached tokens from `input`.
Count reasoning tokens separately only when the agent reports them separately.
When the agent supplies a total, check that the four usage fields reproduce that total.
Set `turns` to the request count, or `null` when the agent omits that count.

Record every tool call, including calls nested inside tool results.
Add `path` for reads and `command` for shell calls.
Normalize skill reads to the supplied absolute skill directory.
When the host loads a skill by name, record the corresponding `SKILL.md` read.

Exit zero when a complete measured result exists, even if the agent's task fails.
Exit nonzero when usage is unavailable or the result is incomplete.
Remove temporary files outside the output directory on normal exit and termination.

## Verification

Run `eval.mjs calibrate <dir>` before accepting the adapter.
Calibration checks the supplied skill, absence of other copies, and an actual shell call.
Calibration does not prove exact token accounting or prevent an agent from finding hidden files.
