# Evidence protocol

## Claim labels

- **AS-IS**: a bounded fact directly located in the pinned revision, or a behavior reproduced under an exact environment and input. Every AS-IS claim requires evidence IDs.
- **INFERRED**: a responsibility, invariant, reason, risk, or unexecuted behavior derived from facts. Show the reasoning chain, alternatives, and counterevidence. High confidence does not convert an inference into AS-IS.
- **UNKNOWN**: evidence is missing, conflicting, unreachable, variant-dependent, generated elsewhere, or runtime-selected. State why, impact, and evidence needed to close it.

Confidence is separate: HIGH means independently corroborated and tightly bounded; MEDIUM means one direct source or strong inference with uncovered edges; LOW means indirect, incomplete, or environment-sensitive.

Crosswalk to `detailed-design-writing`: `AS-IS` maps to `CONFIRMED`, `INFERRED` maps to `INFERRED`, `UNKNOWN` maps to `OPEN`, and optional future changes map to `PROPOSED`. The reverse label and writing status remain separate dimensions.

## Evidence by question

- Current behavior in one scenario: E2 reproduced observation, bounded by input/environment, corroborated with E1 implementation.
- Checked-in but unexecuted test: E1 direct repository artifact with `artifactRole: test`; it proves the test scenario and asserted oracle exist at the revision, not that the program passed or exhibited the behavior.
- Possible paths: E1 source plus actual build/config and semantic/static analysis; a runtime trace covers only a subset.
- Contract or persistent format: schema/IDL/migration/validation/serialization and compatibility tests.
- Rationale: accepted ADR/PR/review/issue/commit. Source proves behavior, not motive.
- Historical origin: complete Git history plus PR/issue; blame is only a lead.
- Absence: a closed, replayable search across relevant control, data, configuration, generation, variant, and dependency space.

## Minimum evidence record

```text
Evidence ID
Claim/behavior IDs
Class: E1 | E2 | E3 | E4 | E5
Artifact role: implementation | schema | config | generated | test | runtime | history | documentation | analysis
Label: AS-IS | INFERRED | UNKNOWN
Confidence: HIGH | MEDIUM | LOW
Repository and full revision
Path, symbol, line range, blob hash or immutable URL
Extraction command/query and tool version
Environment, flags, input and build variant
Raw result excerpt or artifact hash. For source-only E1, the Git blob hash satisfies artifact integrity; set `resultHash` to null with a reason when no separate command output was captured
Scope and limitations
Conflicting evidence IDs
```

Prefer `commit + path + symbol + lines + blob` because line numbers drift even when a claim is still true.

## Triangulation

Critical cross-layer claims should use at least two independent evidence types when possible. E5 analysis artifacts never stand alone. Tests prove only their inputs and assertions; mocks may conceal actual boundaries. Documentation proves what is declared, not what is implemented.

## Negative evidence

A valid bounded negative record contains:

- pinned revision and selected variant;
- search universe and excluded paths;
- exact queries and semantic/static tools;
- submodule, LFS, generated-code, plugin, reflection, and external dependency status;
- result count and saved output hash;
- why the examined universe is closed.

If any material dimension is open, write UNKNOWN instead of “does not exist.”

## Conflict handling

Record conflicts across source, tests, observations, docs, and history. Do not resolve them using a fixed global priority:

- execution answers one scenario;
- source/build answers possible paths for one variant;
- schema and serializers answer representation and compatibility;
- history answers intent;
- docs answer declared behavior.

If a conflict changes interface, state, consistency, security, recovery, or completion, stop at PARTIAL or BLOCKED.

## Closure status

Use exactly one:

- `IMPLEMENTATION CLOSURE ACHIEVED FOR SCOPE S / REVISION R / VARIANT V`
- `PARTIAL RECONSTRUCTION — NOT COMPLETE`
- `BLOCKED — CRITICAL EVIDENCE UNAVAILABLE`

Dynamic execution being disabled or unauthorized does not by itself force PARTIAL. It does force PARTIAL when a critical behavior depends on runtime selection and static evidence cannot close the ambiguity.

Time or token budget exhaustion is never evidence of closure.