# Detailed design methodology

## Positioning

A useful detailed design document is not mainly about writing a long solution narrative.

It should make three things explicit:

- what the system already supports
- what still separates the current system from the target
- how those gaps will be closed in implementation

If those three things are unclear, scope drift and rework become much more likely.

## Writing order

### 1. Start with current capability and boundary

Before describing the solution, explain:

- what is already supported
- what is not yet supported
- where the capability boundary currently is
- what limits exist today

This defines the starting point.

### 2. Define the target capability

State what the change is meant to achieve. Keep the target concrete.

### 3. Perform gap analysis

List the differences between current and target:

- missing capabilities
- uncovered modules or flows
- consequences if the gaps remain

This section explains why the change is needed.

### 4. Map the gaps to implementation

Each important gap should map to a practical implementation direction:

- module updates
- logic additions
- interface changes
- configuration, database, deployment, or process changes

This section explains how the design becomes code and delivery work.

## Recommended structure

```text
1. Background and goals
2. Current state and capability boundaries
3. Target capability
4. Gap analysis
5. Implementation design for each gap
6. Impact analysis
7. Risks and pending confirmation items
8. Delivery plan
```

## Critical rules

### 1. Boundaries must be explicit

Do not write only "support Docker deployment." State the actual scope, such as:

- database-only Dockerization
- full frontend, backend, and database Dockerization

### 2. Known changes need confirmation closure

A design document is not complete just because it was shared once.

Known changes should be visible with:

- what changed
- what scope is affected
- whether it should be done
- whether the boundary is confirmed

### 3. Pending decisions must be separate

Anything needing sign-off should appear under a dedicated pending confirmation section rather than being buried in paragraphs.

## One-line summary

The best detailed design documents explain the current boundary first, then the gap to the target, then the implementation mapping for closing that gap, while keeping important change confirmations visible.
