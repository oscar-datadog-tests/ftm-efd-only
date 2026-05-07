# QA card — ftm-efd-only

## Description

EFD turned on, PR Gate not configured. Drives the "you have detection but no enforcement" branch.

## Audit cells exercised

- §3.4 #3 next-action — "Next: Prevention. Add a PR Gate to block new flaky tests."
- §5.2 #3 prevention verdict — "EFD is detecting flakes, but {N} flaky tests merged this month."
- §5.2 #4 prevention verdict — "Early Flake Detection is active. Add a PR Gate so new flaky tests can't merge."

## Required Datadog toggles

| Toggle | State | Notes |
| --- | --- | --- |
| EFD | **on** | Repo settings |
| PR Gate | **off** | No rule covers this repo |
| ATR | **off** | Repo settings |
| Policies | **none** | Default policy off |

## Special setup steps

None.

## Expected verdicts (after warm-up)

- §3.4 next-action: "Next: Prevention. Add a PR Gate to block new flaky tests."
- §5.2 prevention verdict: depends on `newFlakyTests`. With N>0: §5.2 #3. With N=0: §5.2 #4.

## Readiness

T+14 — needs `newFlakyTests` to be populated by EFD over a month-window.

## How to refresh

```bash
git commit --allow-empty -m "rerun" && git push
```
