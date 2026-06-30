# orca-app-store-preflight

## Purpose

Prepare an Apple app submission pack that is actually review-ready before upload or App Store review.

This command closes the gap between "the build works" and "Apple can review, understand, and approve the submission."

## When To Use

Use before:

- first App Store submission for a new app
- App Store update submission
- TestFlight builds that need complete beta review info or external distribution
- release work where Apple metadata, legal links, privacy declarations, screenshots, or review notes may block approval

## Required Inputs

- repo path
- platform target such as iOS, iPadOS, macOS, watchOS, or visionOS
- submission type: `new_app`, `update`, or `beta_only`
- bundle id
- version and build target

## Optional Inputs

- project/workspace path
- scheme
- existing `fastlane/` folder
- App Store Connect app identifier
- release notes or "What's New" draft
- legal/support URLs
- paywall or subscription screenshots
- reviewer credentials

## Linear Context

- Expects: release issue, ship target, current release evidence, linked QA/review findings, legal/privacy blockers, and upload state
- Reads: ship checklist, review findings, QA evidence, release notes, and known blockers
- Posts: App Store preflight result, missing items, release-state recommendation, and exact submission blockers
- Trigger: Apple release work that is nearing upload, TestFlight distribution, or review submission
- Human approval: required to waive blocking App Store review risks or knowingly ship with incomplete operator evidence

## Opt-Out Context

Write the preflight result to the chosen record before the Apple release continues.

## Workflow

1. Use `orca-app-store-preflight`.
2. Classify the lane:
   - new app submission
   - app update submission
   - TestFlight beta-only distribution
3. Audit product/runtime readiness:
   - debug or placeholder content removed
   - purpose strings are specific
   - privacy manifest and data-use claims match reality
   - account deletion exists when accounts exist
   - restore purchases exists when IAP exists
   - production cloud/backend state is live, not test-only
   - non-obvious reviewer flows are documented
4. Audit App Store Connect completeness:
   - name, subtitle, description, keywords, category, pricing, availability
   - privacy policy, support URL, and other legal/support links
   - age rating, content rights, export-compliance answers, and release mode
   - screenshots and app previews for supported device families
5. Audit review-facing materials:
   - App Review notes
   - test credentials or demo path
   - screenshots proving sensitive controls such as delete account, restore purchases, or paywall details
   - explanations for non-obvious features or IAP visibility
6. Audit commerce and trust surfaces:
   - exact price and billing frequency
   - free-trial clarity
   - cancellation instructions
   - deceptive UI risk
   - support contact visibility
7. Map the submission to operator artifacts:
   - `fastlane precheck` metadata lint
   - `fastlane deliver` metadata, screenshots, app previews, review information, submission information
   - `fastlane pilot` beta app review info, localized app info, groups, and What to Test
8. Fill the submission pack artifact and explicit blocker list.
9. Route unresolved blockers to `orca-review`, `orca-design`, `orca-security-check`, `orca-testflight-ops`, or `orca-ship` as needed.

## Outputs And Artifacts

- `templates/app-store-submission-pack.md`
- `templates/app-store-review-notes.md`
- App Store preflight summary

## Failure Cases

- If release state is only "local build passed", do not call the app submission-ready.
- If privacy/legal URLs are missing or inconsistent, block submission.
- If the app requires login and reviewer access is missing, block submission.
- If screenshots, app previews, or review notes are stale after meaningful UI changes, block submission.
- If IAP, subscriptions, restore flow, or cancellation guidance are unclear, block submission.

## Related Commands And Skills

- Commands: `orca-ship`, `orca-review`, `orca-design`, `orca-security-check`, `orca-test-briefed`, `orca-testflight-ops`
- Skills: `orca-app-store-preflight`, `orca-ship`, `orca-testflight-release`, `orca-testflight-ops`
