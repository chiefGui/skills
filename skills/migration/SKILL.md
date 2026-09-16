---
name: migration
description: Use only when explicitly invoked to record or execute a project migration.
---

# Migration

## Shared rules

- Store records in `.migration/` at the project root, named `YYYY-MM-DD-short-title.md`.
- `pending/` contains outstanding execution, recovery, or verification.
- `completed/` contains permanent history of verified final outcomes with no outstanding work.
- Update the same record throughout its lifecycle.
- Keep only migration-specific information needed to execute, resume, verify, or understand the outcome. Omit empty sections, generic advice, duplicated context, and unrelated logs.
- Resolve questions from code, records, and target state. Ask the user only for information or decisions that cannot be established independently.
- Defer implementation until Execute. Temporary execution artifacts are disposable; records persist.

## Record

- Inspect the relevant implementation and existing records.
- Create a pending record, or update the existing entry for the same migration, with:
  - Required change, reason, and intended result.
  - Affected state and intended environments.
  - Dependencies and timing relative to deployment.
  - Observable conditions for success.
  - Known constraints and unresolved decisions.
- Delete an obsolete entry only if execution never started.
- If an obsolete migration has started, preserve its history, establish the revised intended state and remaining work for every affected target, and finish through Execute.

## Execute

### Prepare and preflight

- Read the pending record and check its assumptions against the current implementation and target state.
- Identify the exact target, affected scope, and work already applied.
- Check required access, dependencies, deployment ordering, and any concurrent writes or running application versions that affect correctness.
- Prepare the execution method, including safe retry or resumption after partial failure and recovery from destructive changes.
- Verify that required recovery resources are available and usable.
- Validate the approach using read-only checks, dry runs, or isolated tests appropriate to the change. Ensure validation cannot modify the target.
- Define success checks and conditions that require stopping.
- Save the prepared plan, preflight evidence, and remaining uncertainty in the pending record.

### Approval

- Present the target, scope, intended changes, preflight results, unverified assumptions, expected disruption, recovery provisions, and success checks. Omit inapplicable details.
- State whether execution is ready and why. Resolve blockers to correct execution or verification before requesting approval.
- Ask for explicit approval of the prepared plan and wait. Do not modify the target before approval.

### Run and verify

- Recheck preflight assumptions that may have changed. If changes invalidate the approved plan, repeat the affected preparation and obtain renewed approval.
- Execute the approved plan; stop on defined stop conditions or behavior outside the plan.
- Record when and where execution occurred, what was executed, and results and verification evidence per target. Preserve partial progress and enough detail to resume safely; identify cancellations or reversals explicitly.
- Keep the record pending until every affected target reaches its intended state and passes verification.

### Finalize

- Replace plans with what actually happened. Remove resolved questions, superseded instructions, and working notes; preserve relevant decisions, deviations, and verification evidence.
- Move the record to completed, then remove temporary execution artifacts.
