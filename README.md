# Requirement Replacement Guard

A standalone Codex skill for replacing, removing, deprecating, or forbidding behavior without allowing stale requirements to survive or return later.

It turns a change request into a final-state contract, checks the full impact surface, keeps retired concepts out of current-code rationale, and requires positive tests, negative verification, and reviewed residual searches.

## Install

PowerShell:

```powershell
git clone https://github.com/WH2020/requirement-replacement-guard.git "$env:USERPROFILE\.codex\skills\requirement-replacement-guard"
```

macOS or Linux:

```bash
git clone https://github.com/WH2020/requirement-replacement-guard.git ~/.codex/skills/requirement-replacement-guard
```

## Use

```text
$requirement-replacement-guard Replace the legacy option with the new behavior and verify that no stale paths, defaults, tests, or documentation can bring it back.
```

The skill is intentionally independent of ReqGuard and does not require project-specific workflow documents or scripts.

## Automatic invocation

Implicit invocation is explicitly enabled in `agents/openai.yaml`. Codex initially matches an installed skill from its name and `description`, so the description front-loads the intended semantic triggers and the important exclusions.

Likely automatic matches:

- "删除这个旧功能，并确保以后不会重新加回来。"
- "这个字段已经废弃，清理代码、测试、默认值和文档。"
- "Replace the legacy option and prove the old path cannot be reached."
- "The removed fallback returned; remove every stale path and add a regression test."
- "This value must never be generated again."

Expected non-matches:

- "Add a new export format."
- "Delete this temporary file."
- "Move these files without changing behavior."
- "Explain why the legacy feature was removed."

Automatic selection is model-routed rather than a deterministic keyword hook. Use explicit `$requirement-replacement-guard` invocation when a workflow must be selected with certainty.
