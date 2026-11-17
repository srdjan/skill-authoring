# Command formats

Write examples in the syntax the agent actually sends.
Use usage lines for shell commands, signatures for SDK calls, and JSON shapes for native tools.
Keep allowed values and defaults next to the relevant argument.
Use a short comment only when the command cannot express the constraint.

```text
CLI:     select <ref> <value> [--by value|label|index]
SDK:     select(ref: string, value: string, options?: { by?: "value" | "label" | "index" })
Native:  {"ref":"item","value":"choice","by":"label"}
```

Give common operations complete examples.
Give difficult argument shapes one tested example.
List the remaining operation names without copying their reference documentation.
Do not claim a format saves tokens without measuring the relevant model tokenizer.
