# Task packets and review prompts

Read this reference when preparing a Luna implementation packet or an independent Terra review. Use the dispatcher skill for the full worker lifecycle and isolation contract; keep this file focused on task-specific acceptance, Ponytail, and review fields.

## Implementation packet

```text
Worker / task / wave
- <worker ID> / <task ID> / <wave number>

Objective
- <one observable result>

Workspace and baseline
- Work only in: <absolute isolated path>
- Baseline: <immutable revision/hash>

Authoritative inputs
- <task card/spec>
- <code/schema entrypoints>
- <Figma node/demo/screenshot when applicable>

Ponytail solution gate
- Intensity: <full unless the user explicitly chose another level>
- Complete affected flow: <entry → state owner → side effects → result/verification>
- First sufficient rung: <no change / reuse / standard library / native platform / installed dependency / one direct line / minimum new code>
- Explicit non-goals: <abstractions, dependencies, configuration, scaffolding, or adjacent cleanup not required>
- Deliberate ceiling: <none, or `ponytail:` comment with the known ceiling and upgrade trigger>
- Bug fix owner: <all callers inspected; shared root cause location, or not applicable>
- Non-trivial logic: <one minimal runnable check; supplements rather than replaces required project validation>

Allowed changes
- <exact files or globs>

Forbidden changes
- No commit/push/deploy/dependency upgrade/broad formatting.
- Do not edit <unrelated or user-owned paths>.
- Do not spawn nested agents or delegate the task.

Acceptance
- <behavioral and structural checks>
- <reference-fidelity checks>

Verification
- <exact commands>

Return
- Actual changed paths, concise rationale, command outputs, risks, and blockers.
- Do not report completion without a real filesystem diff unless the baseline already passes every acceptance check; prove that case explicitly.
```

## Domain/state reviewer

Perform a read-only review of the current candidate against the authoritative task/spec. Inspect the actual source and diff. Check invariants, state ownership, transitions, authorization, idempotency, concurrency, side effects, historical facts, and rollback. Do not modify files. Report only actionable P0/P1/P2 findings with tight file/line evidence; if none remain, say so explicitly.

## Schema/integration reviewer

Perform a read-only review of the current candidate against the authoritative task/spec. Inspect runtime schema semantics, generated types, compatibility, request/response/error exits, call-site or migration chains, validation commands, and cross-layer consistency. Do not modify files. Report only actionable P0/P1/P2 findings with tight file/line evidence; if none remain, say so explicitly.

## Delivery/reference reviewer

Perform a read-only delivery review of the current candidate against the task packet and named source-of-truth references. Check scope, regression risk, tests, missing loading/empty/error/permission states, Figma/demo structure and layout fidelity when applicable, unjustified abstractions/dependencies/scaffolding, cleanup, and recovery. Do not recommend optional refactors that do not fix an acceptance gap. Do not modify files. Report only actionable P0/P1/P2 findings with tight file/line evidence; if none remain, say so explicitly.

## Final full review

Use the same raw task packet and latest artifacts. Do not include an earlier defect list or tell the reviewer what was fixed. Ask for a complete read-only review, not confirmation of expected fixes.
