# Tool routing

Use the strongest available safe tool, record its version and limitations, and never auto-install tools.

| Need | Preferred | Fallback | Caveat |
|---|---|---|---|
| Files | `rg --files`, `git ls-tree` | `find` | Generated/ignored/LFS files may be absent |
| Text | `rg`, `git grep` | `grep` | Name matches are seeds, not membership proof |
| Symbols | compiler/LSP/SCIP index | ctags/tree-sitter, text references | Dynamic dispatch, reflection, macros, DI can be incomplete |
| Control/data flow | compiler DB, CodeQL, language AST/data-flow | manual callers/callees and slices | Static results may over- or under-approximate |
| Build variant | CI, lockfile, manifest, compile database | documented commands | Wrong flags produce the wrong program model |
| Tests | existing focused tests and assertions | characterization harness | Running code requires the dynamic safety gate |
| Runtime | trace, logs, coverage, state diff | static evidence | One execution is not universal behavior |
| History | `git log -S/-G/-L`, `show`, move/copy-aware blame | current snapshot | Shallow/squashed/vendor history is incomplete |
| External docs | official docs and upstream specs | repository docs | External version must match pinned implementation |
| Diagrams | evidence-linked C4/dynamic/state/data models | Markdown tables | Diagrams express the model; they do not prove it |

## Feature-location passes

1. Inventory languages, packages, build, configuration, schemas, tests, and entry surfaces.
2. Search observable strings and identifiers.
3. Follow semantic definitions/references/implementations and registration sites.
4. Trace forward from inputs and backward from results/state writes/assertions.
5. Search tests, mocks, snapshots, fixtures, migration, deployment, and telemetry.
6. When multiple value sources or writers share a destination, recover source-resolution and conflict/arbitration as separate orderings.
7. Inspect history for origin and rationale.
8. Search for counterexamples and alternative paths.
9. Classify every remaining frontier.

For huge repositories, build a symbol/reference map and rank likely feature neighborhoods to control context. A map is a navigation index, not evidence.

## Generated and external code

Trace generator inputs, generator/version/command, output, and consumers. Record inability to regenerate or diff as a stale-risk UNKNOWN. For external packages, pin version/source and stop at a declared contract boundary unless their implementation is essential and available.

## Diagrams

Use C4 context/container/component/code views only as needed, plus feature-specific dynamic sequence, state machine, and data lineage. Attach evidence IDs to nodes and edges; mark inferred relationships.