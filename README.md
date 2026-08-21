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
