---
name: detailed-design-writing
description: Write, extend, review, or restructure detailed design documents. Use when the user wants help describing current capability boundaries, target capability, gap analysis, implementation mapping, risks, or approval items in a detailed design.
---

Use this skill when the user needs help writing or refining a detailed design document.

The goal is not to make the document longer. The goal is to make scope, boundaries, gaps, implementation mapping, and confirmation items explicit so the design can actually guide delivery and avoid rework.

## When to use

Use this skill when the user asks for things like:

- write a detailed design document
- improve a detailed design
- how to structure a detailed design
- what the current system already supports
- what the target still lacks
- how to map design gaps into code changes
- how to list risks or approval items

## Core principles

### 1. Write current state and boundaries before the solution

Do not jump straight to "what we will do."

First make these things explicit:

- what the system already supports
- what it does not support
- where the current capability boundary is
- what the current constraints are

### 2. Define the target capability clearly

State what this change is supposed to achieve. Avoid vague goals that hide scope questions.

### 3. Keep gap analysis as a separate section

Do not skip directly from current state to implementation.

The design should explicitly say:

- what capabilities are still missing
- what modules or flows do not cover the target
- what would go wrong if those gaps are not addressed

### 4. Map every important gap to implementation

Do not stop at "what is missing." Also say "how it will be closed."

Try to map each important gap to:

- module changes
- interface changes
- data or configuration changes
- deployment or process changes
- code-level landing points

### 5. Keep confirmation items visible

Known changes should not be assumed to be approved just because they were mentioned somewhere.

If a scope decision, boundary, or impact still needs confirmation, list it clearly under pending confirmation items.

## Recommended structure

Unless the user already has a template to follow, organize the design like this:

1. Background and goals
2. Current state and capability boundaries
3. Target capability
4. Gap analysis
5. Implementation design for each gap
6. Impact analysis
7. Risks and pending confirmation items
8. Delivery plan

## Working flow

1. Extract the user's actual goal.
2. Describe what the current system already supports and does not support.
3. Make the boundary explicit, especially where scope is easy to misunderstand.
4. Split out the gap between current and target.
5. Map the important gaps into implementation.
6. List risks and pending confirmation items separately.
7. If needed, add a management-facing summary for reporting.

## Output rules

When producing a detailed design or outline, optimize for:

- clear scope
- clear boundaries
- clear gaps
- clear implementation mapping
- clear approval items

Do not return a generic empty template if the user has already given enough project context to fill sections concretely.

## Strong reminders

### Do not blur deployment scope

For example, do not write only "support Docker deployment." Be explicit about whether the scope is:

- database only
- frontend, backend, and database together

### Do not bury pending decisions in body text

Anything that needs a decision from leadership, product, test, or ops should be listed explicitly.

### Do not confuse mention with confirmation

Mentioned in a chat, said in a meeting, or understood by the team does not automatically mean formally confirmed.

## References

Read `references/methodology.md` for the longer methodology.
Read `templates/detailed-design-template.md` for a reusable structure.
