---
name: ai-delivery-loop
description: Run a full delivery loop for a requirement: research, design, TDD implementation, acceptance mapping, and review iteration. Use when the user wants one AI workflow to carry a feature from unclear requirement to final review-ready delivery.
---

Use this skill when the user wants a single workflow that covers requirement research, solution comparison, design, coding, acceptance, and review.

## Non-negotiables

- All working docs must use plain language. Avoid jargon unless the user asks for it.
- Do not jump into coding until the requirement has been grilled and the design has explicit scope boundaries.
- Tests are not optional. Strict TDD is preferred. At minimum, tests must clearly guard the intended behavior.
- Review findings must flow back into the design doc, then back into code and verification.

## Phase 1: Research

Before doing anything else, activate `grill-me` on the requirement summary.

- Ask one question at a time.
- For each question, give a recommended answer.
- If a question can be answered by inspecting the repo, inspect the repo instead of asking.
- Keep drilling until these axes are clear:
  - business goal
  - scope and out-of-scope
  - complexity preference
  - deployment and environment expectations
  - architecture and platform constraints
  - acceptance standard

If `grill-me` is unavailable in the current environment, say so clearly and then emulate its behavior: ask short, branching, assumption-hunting questions one by one until the same clarity is reached.

After clarification, produce multiple solution layers.

### Solution set to produce

#### Plan 1: Prototype version

This is the smallest working path.

- Ignore fault branches, degraded paths, and edge cases.
- Only solve the happy path in the current environment.
- Use the fewest moving parts possible.
- Good for feasibility checks, quick probing, and unblocking design uncertainty.

Typical example for a Vue + Go project:
- Prepare: install dependencies
- Build: compile frontend and backend in the simplest way
- Package: produce the most direct runnable artifact

#### Plan 2: Engineered version

This is the serious implementation candidate.

Include:
- dependency setup
- failure handling
- error branches
- environment differences
- deployability
- operational concerns

#### Plan 3 and beyond: Industry research variants

Research real-world practice and produce more options.

Examples:
- mainstream build and packaging patterns
- multi-environment deployment patterns
- multi-arch build strategies
- common CI/CD layouts
- reliability hardening patterns

Name them as `方案三`, `方案四`, `方案五` and so on.

### What to confirm with the user

At minimum, resolve:
- whether they only want simple error handling or production-grade dependency and failure handling
- whether they only need the current machine architecture or need cross-platform / multi-arch output
- whether prototype code should be written during research to de-risk unknowns

### Research output

Produce a research note in plain language that includes:
- requirement summary
- clarified assumptions
- comparison table or bullet comparison of each plan
- recommendation and why
- unresolved risks

## Phase 2: Design

Turn the chosen research result into one unified design.

The design doc must include:
- target behavior
- module breakdown
- data flow or request flow when relevant
- boundary conditions
- failure and error paths
- test strategy
- rollout or integration notes when relevant

Also design test cases here, not later.

For each important behavior, define:
- what should happen
- what must not happen
- how a test will prove it

### Optional prototype track

If there is still uncertainty, write prototype code based on Plan 1.

Rules for prototype code:
- optimize for speed of learning, not maintainability
- no need for complete tests
- no need for full error handling
- it is acceptable to throw the prototype away after design is refined

## Phase 3: Coding

Implement from the design doc.

### Coding rules

- Prefer TDD: write or update the test first, then implement.
- If strict TDD is not practical, still ensure tests are added before closing the task.
- Map each design feature to concrete code modules.
- For new functionality, create the needed infrastructure as well, such as routes, pages, handlers, configs, and integration points.
- Follow the repo's existing conventions unless the design explicitly calls for a change.

### Coding output

Keep a running mapping of:
- design item
- implementation location
- guarding test

## Phase 4: Acceptance

Do not treat acceptance as "tests passed" only.

Create a verification note that maps:
- design feature
- code implementation
- test coverage
- manual verification status

This note must be written in plain language so a human can read it quickly.

Acceptance should catch mismatches such as:
- design mentions compile + deploy, but code only implements deploy
- design expects error handling, but code only covers the happy path
- tests exist, but they do not guard the real user-facing behavior

## Phase 5: Review and Iteration

Run review from multiple perspectives when possible.

Priority review angles:
- failure scenarios
- error handling
- robustness
- compatibility gaps
- missing tests
- design / implementation mismatch

If multiple models or review agents are available, run them in parallel. Treat their outputs as review inputs, not final truth.

### Review loop

For every meaningful review finding:
1. update the design doc first
2. add or update tests
3. implement the fix
4. manually verify the affected behavior when needed
5. append the result to the verification note
6. re-run review if the change opens new risk

## Completion standard

The task is done only when all of these are true:
- requirement ambiguity has been grilled down to an actionable scope
- a chosen design exists and matches the implementation
- tests guard the important behavior
- verification notes map design to code in plain language
- review findings have been fed back and closed in a documented loop

## Default deliverables

Unless the user asks otherwise, produce these artifacts:
- research note
- design doc
- tests
- implementation
- verification note
- review findings summary

## Response style

When using this skill:
- explain trade-offs plainly
- prefer concrete examples over abstract theory
- call out uncertainty early
- keep docs human-readable
- do not bury risks under polished wording
