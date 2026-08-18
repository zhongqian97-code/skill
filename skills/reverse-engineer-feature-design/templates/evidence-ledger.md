# Evidence ledger templates

## evidence.jsonl

One JSON object per line:

```json
{"evidenceId":"E-0001","behaviorIds":["BEH-001"],"claim":"bounded claim","class":"E1","artifactRole":"implementation","label":"AS-IS","writingStatus":"CONFIRMED","confidence":"HIGH","repo":"https://github.com/owner/repo","revision":"full-sha","variant":"profile/platform/flags","path":"src/file.ext","symbol":"Namespace.Type.method","lines":"120-168","blob":"blob-sha","permalink":"immutable-url","command":"sanitized replay command","tool":"tool version","environment":"relevant non-secret context","input":"scenario input","resultHash":"sha256:... or null","resultHashReason":"required when null; Git blob may provide source integrity","excerpt":"minimal excerpt","limits":["not executed"],"conflicts":[]}
```

## search-log.jsonl

```json
{"searchId":"S-0001","revision":"full-sha","purpose":"locate retry behavior","query":"exact query","tool":"rg version","universe":["src/","tests/","config/"],"excluded":[],"variants":["selected variant"],"submodules":"not initialized","generated":"included/excluded and why","hits":3,"resultHash":"sha256:...","conclusion":"bounded conclusion only"}
```

## conflicts.md

| ID | Claim | Evidence A | Evidence B | Affected semantics | Current disposition | Evidence needed |
|---|---|---|---|---|---|---|

## feature frontier

| Node/edge | Why relevant | Status | Boundary reason | Evidence | Next action |
|---|---|---|---|---|---|

Allowed status: `expanded`, `shared boundary`, `external boundary`, `excluded`, `UNKNOWN`.

## behavior traceability

| Behavior ID | Entry | Control/data/state | Side effects | Output/error | Tests/observations | Evidence IDs | Status |
|---|---|---|---|---|---|---|---|

## Phase summary minimum

- Phase name and status
- Full revision and selected variant
- Scope covered
- Evidence IDs added
- Searches and commands performed
- Decisions made
- Conflicts and UNKNOWNs
- Next actions
