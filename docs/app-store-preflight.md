# App Store Preflight

ORCA Framework already had Apple upload and TestFlight operations lanes.

The missing layer was the operator-complete submission pack between:

- "the binary archives and uploads"
- and "Apple can actually review and approve this without bouncing it for missing operator work"

`orca-app-store-preflight` closes that gap.

## What It Covers

The preflight is broader than code compliance.

It checks:

- product/runtime readiness
- App Store Connect metadata completeness
- screenshots and app previews
- privacy, legal, and support surfaces
- paywall and subscription clarity
- reviewer credentials and App Review notes
- TestFlight beta review info
- export-compliance, rating, release-mode, and submission toggles

## Why This Exists

Most Apple release failures are not "Xcode could not archive."

They are things like:

- no reviewer login
- stale screenshots after a UI rewrite
- support or privacy URL missing
- no restore-purchases path
- account deletion not easy to find
- vague paywall terms
- non-obvious features not explained in review notes
- beta metadata or What to Test never updated

ORCA should treat those as first-class release blockers, not as afterthoughts.

## New App Versus Update

The preflight explicitly splits:

- `new_app`
- `update`
- `beta_only`

That matters because:

- new apps need full listing, category, pricing, screenshot, and legal setup
- updates need accurate What's New text, changed-flow screenshots, and refreshed review notes
- beta-only lanes often need What to Test, beta review info, and tester-group state more than full App Store submission state

## Fastlane Mapping

The preflight is designed to map onto the strongest existing operator surfaces:

- `fastlane precheck`
  - metadata lint such as placeholder text, missing current-year copyright, and IAP description mismatches
- `fastlane deliver`
  - metadata
  - screenshots
  - app previews
  - review information
  - privacy/support URLs
  - submission information
  - app rating config
  - automatic or phased release settings
- `fastlane pilot`
  - What to Test
  - beta app review info
  - localized beta app info
  - tester groups
  - external distribution

## Apple-Specific Risk Areas

These should block the release when incomplete:

- privacy policy missing from App Store Connect or in-app
- account deletion required but unavailable
- digital purchases bypassing IAP rules
- restore purchases missing
- misleading price, trial, or cancellation language
- Kids Category or child-data handling mistakes
- stale or inaccurate metadata, screenshots, or previews
- reviewer credentials missing when login is required
- export-compliance or content-rights answers left implicit

## Core Artifacts

Use:

- [../templates/app-store-submission-pack.md](../templates/app-store-submission-pack.md)
- [../templates/app-store-review-notes.md](../templates/app-store-review-notes.md)

## References

Primary references that shaped this lane:

- Apple App Store Review Guidelines: <https://developer.apple.com/app-store/review/guidelines/>
- fastlane `precheck`: <https://docs.fastlane.tools/actions/precheck/>
- fastlane `deliver`: <https://docs.fastlane.tools/actions/deliver/>
- fastlane `pilot`: <https://docs.fastlane.tools/actions/pilot/>

Useful checklist references:

- <https://github.com/lukylab/appstore-submission-checklist>
- <https://github.com/xrazz/app-store-approval-guide>
