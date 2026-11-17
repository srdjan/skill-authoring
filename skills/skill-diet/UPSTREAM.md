# Upstream provenance

Source: <https://github.com/nicobailon/skill-diet>.
Commit: `5f41df1220eb5759c413390206f1b9e6c63be754`.
Inspected on 2026-10-27.
The upstream MIT license is preserved in `LICENSE`.

The adoption uses `SKILL.md`, all five references, `scripts/eval.mjs`, and `scripts/observe.mjs`.
The upstream README and package metadata informed the runtime and distribution review.
The original Gotai adoption used a registry and generators for distribution.
The standalone extraction uses the layout described in the root README.
Upstream package manifests and release tooling are not imported.

The prose follows this repository's ASD-STE100 rules.
The entrypoint routes every resource and includes the required Maintenance block.
The maintenance workflow records bytes without calling bytes tokens.
The evaluation guidance states the limits of text assertions and calibration.

The scripts keep the upstream JavaScript modules and Node built-in imports.
Deno supplies the compatibility APIs; no Node installation or dependency download is required.
Local changes replace runtime commands and shim generation with Deno commands.
The scorer rejects incomplete result matrices instead of returning success for missing runs.
The evaluator rejects an unknown flag, and a flag without its value, with exit code 2.
The original repository has CLI tests for those adaptations and the synthetic evaluation pipeline.

Synthetic tests do not establish live model quality or token savings.
No reduction of the existing skill corpus forms part of this adoption.
