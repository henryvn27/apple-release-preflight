# Apple Release Preflight

Submission-readiness pack for TestFlight and App Store review. It covers metadata, privacy/legal surfaces, screenshots, review notes, reviewer credentials, beta info, and release blockers.

This tool was extracted from the retired `hvn-stack` repo and is wired into the overall manager catalog through [orca-tool.json](orca-tool.json).

Parent manager: https://github.com/henryvn27/orca-framework

## What It Provides

- App Store submission preflight command
- App Store submission pack template
- App Review notes template
- iOS simulator / Apple release reference docs

## Verify

```sh
test -f commands/orca-app-store-preflight.md && test -f skills/orca-app-store-preflight/SKILL.md && test -f templates/app-store-submission-pack.md
```

## Proof

See [PROOF.md](PROOF.md).

## Progress HTML

This repo has a root [progress.html](progress.html) status surface.

Agent rule: if `progress.html` exists, update it after meaningful lifecycle changes and before final response. Keep the current goal, Do next, progress bar, latest update, slice/chunk states, timestamps, next actions, and verification evidence current. Do not install hooks, watchers, daemons, or wrappers.
