# Detect Playbook

## Objective

Identify formulaic AI writing patterns in the user's draft without rewriting,
scoring, or claiming who authored it.

## Detection

Inspect only the supplied prose. Use the relevant direct catalogs:

- [phrases.md](phrases.md) for filler and phrase-level tells.
- [structures.md](structures.md) for repeated rhetorical structures and rhythm.
- [tropes.md](tropes.md) for word, sentence, paragraph, tone, and format tropes.
- [examples.md](examples.md) when one comparison clarifies a finding.

Treat every pattern as contextual evidence. Do not flag an unusual phrase only
because it appears in a catalog. Preserve intentional voice, domain language,
genuine emphasis, uncertainty, and spoken rhythm.

## Output Contract

For each finding, provide the pattern name, an offending excerpt of no more
than 125 characters, and a one-line suggested fix. Order findings by their
effect on the prose. Stop after the findings.

Do not rewrite the draft. Do not score it. Do not state or imply whether a human
or model authored it.

## Verification

Confirm that every quoted excerpt occurs in the supplied text and stays within
the length limit. Remove duplicate findings. Check that each suggestion fixes
the named pattern without changing the writer's factual meaning or register.
