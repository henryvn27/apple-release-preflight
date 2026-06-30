---
name: orca-app-store-preflight
description: Build a complete Apple submission pack before TestFlight or App Store review.
---

# App Store Preflight

Use when an Apple app is moving toward TestFlight distribution, App Store review, or release claim that depends on App Store Connect being complete.

## Inputs

- repo path
- platform target
- submission type: `new_app`, `update`, or `beta_only`
- bundle id
- target version/build
- App Store Connect context when available

## Workflow

1. Classify lane: new app, update, beta-only.
2. Check product/runtime readiness.
3. Check App Store Connect metadata.
4. Check privacy, legal, commerce, and support surfaces.
5. Check reviewer notes, credentials, and evidence screenshots.
6. Map findings to fastlane `precheck`, `deliver`, and `pilot` when present.
7. Fill `templates/app-store-submission-pack.md`.
8. Fill `templates/app-store-review-notes.md`.
9. Mark each issue ready, non-blocking follow-up, or blocking.

## Output

- submission pack
- reviewer notes
- blocking list
- exact next command or human decision
