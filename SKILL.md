---
name: requirement-replacement-guard
description: Prevent stale requirements from surviving or returning when a task replaces, removes, deprecates, or explicitly forbids behavior. Use for final-state contracts, compatibility decisions, cleanup inventories, negative verification, and residual-reference review. Do not use for purely additive changes.
---

# Requirement Replacement Guard

Treat requirement replacement and removal as final-state transformations, not local patches to the previous design. Prevent retired behavior from returning through stale code paths, tests, defaults, documentation, comments, generated artifacts, or accumulated task context.

## Scope

Use this skill when a request:

- replaces an accepted behavior or acceptance criterion
- removes a feature, field, option, default, interface, or code path
- deprecates behavior under a temporary compatibility policy
- explicitly forbids something that earlier work allowed or required

Do not use it for purely additive work, ordinary refactoring with unchanged behavior, or historical analysis that does not request a change.

This skill does not authorize destructive migration, compatibility breaks, data deletion, or external changes beyond the user's request.

## Classify the change

Identify the change as one of:

- **Replacement:** new behavior supersedes old behavior.
- **Removal:** old behavior must no longer exist.
- **Deprecation:** old behavior remains temporarily with an explicit retirement condition.
- **Additive:** old behavior remains valid; stop using this skill unless another item is also replaced or removed.

Do not disguise replacement or removal as an additive patch.

## Freeze the final-state contract

Before editing, record a concise contract:

```markdown
Change kind: replacement / removal / deprecation
Supersedes: prior requirements, acceptance criteria, interfaces, or decisions
Final state: observable behavior that must exist
Forbidden residuals: behavior, identifiers, paths, defaults, explanations, or generated output that must not remain
Allowed residuals: historical or compatibility references that may remain, with reasons and retirement conditions
Compatibility policy: break, migrate, reject, ignore, translate, temporarily support, or not applicable
Cleanup surfaces: relevant code, data, tests, documentation, operations, and generated artifacts
Verification: positive checks, negative checks, residual search, and required evidence
```

An explicit, unambiguous user instruction can confirm the new final state. Do not ask the user to reconfirm it unless compatibility, migration, destructive handling, safety, audit retention, or cross-requirement ownership remains materially unclear.

Mark earlier conflicting task assumptions as superseded. Do not carry them into implementation or use them to infer extra requirements.

## Inspect the impact surface

Check applicable surfaces instead of deleting only the visible implementation:

- primary, alternate, fallback, recovery, and generated code paths
- public and internal APIs, types, schemas, serialization, validation, and protocol fields
- configuration, defaults, feature flags, environment variables, build options, and deployment manifests
- migrations, persisted data, caches, upgrades, downgrade paths, and rollback behavior
- tests, fixtures, mocks, snapshots, golden data, fuzz seeds, and test names
- documentation, examples, prompts, templates, comments, errors, telemetry, and dashboards
- requirement status, module ownership, traceability, decisions, and release notes

Search exact names, identifiers, aliases, and likely synonyms. Text search is evidence, not proof: inspect semantic paths that can recreate the retired behavior under different names.

Do not delete required history or audit evidence. List intentional historical matches under `Allowed residuals`.

## Implement the current design

- Implement the final state directly instead of retaining the old model behind a disabled visible branch.
- Remove obsolete tests and comments; do not rewrite them to explain why the retired behavior is unnecessary.
- Keep current-code comments about invariants that remain true.
- Put necessary history in a change record, ADR, changelog, migration note, or release note.
- Preserve compatibility only when the contract requires it.
- Avoid unrelated refactors and inferred product requirements during cleanup.

## Verify absence and presence

Use all applicable checks:

1. Positive tests prove the required final behavior.
2. Negative tests prove retired behavior cannot be selected, generated, accepted, restored, or reached through supported paths.
3. Migration and compatibility tests cover persisted state and external consumers when relevant.
4. Review every residual-search match; remove it or record it under `Allowed residuals`.
5. Review the final diff against the contract, including defaults, tests, documentation, comments, and generated artifacts.
6. Update requirement-to-code-to-test traceability when the project maintains it.

When practical, turn absence requirements into tests, lint rules, hooks, or CI checks. Do not claim complete removal based only on a text search.

## Completion report

Report:

- confirmed final state
- changed and removed surfaces
- positive and negative verification performed
- residual search terms and surviving matches reviewed
- allowed historical or compatibility references
- tests and evidence
- unverified runtime, generated, persisted, or external paths
