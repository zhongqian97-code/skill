# Evidence Protocol

## Coordinates

Pin evidence to a full commit and prefer stable locators:

- repository URL + full commit + path + symbol + line range;
- migration/schema version + object name;
- test name and assertion;
- runtime command/environment/result when authorized;
- history commit or authoritative project documentation.

Line numbers are navigation aids. Symbol, blob/commit, object, and test identity are the durable coordinate.

## Strength

- E1: direct pinned implementation source;
- E2: executable test, migration, DDL, schema, or generated contract;
- E3: authorized runtime observation;
- E4: relevant history or authoritative project documentation;
- E5: inference.

Label conclusions AS-IS, INFERRED, or UNKNOWN. E5 cannot close a material implementation contract by itself.

## Evidence arbitration

When artifacts disagree, record every artifact and the precedence evidence. Typical candidates:

- applied migration/schema dump versus ORM/model;
- runtime validator/router versus type definition or docs;
- producer payload versus consumer assumption;
- executable UI validation/state versus copy or screenshots;
- resolved configuration versus sample files.

Do not assume a generic precedence rule proves this repository's runtime winner.

## Negative evidence

A claim that something is absent must include:

- search scope;
- search terms/patterns;
- excluded generated/vendor paths;
- result;
- plausible blind spots.

## Coverage

Every BEH, INV item, contract, lineage row, database object, and material failure has evidence or an explicit unknown. Evidence count is not coverage; use the closure matrices.

## Source defects versus reconstruction omissions

A source defect is a pinned inconsistency or missing behavior in the implementation and belongs in the appendix/conflict ledger. A reconstruction omission is a source behavior or artifact that exists but is not represented in the document. Do not use source defects to excuse missing reconstruction detail.
