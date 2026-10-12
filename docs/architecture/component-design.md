# Project Umbra — Component Design

**Status:** Proposed architecture; validate against current Gecko APIs before implementation  
**Related baseline:** docs/requirements/browser-requirements.md  
**Platforms:** Windows, macOS, Linux, Android  
**Engine direction:** Gecko / GeckoView

## 1. Design goals

- Separate privileged browser chrome from untrusted web content.
- Centralise privacy decisions rather than duplicating policy in UI widgets.
- Make cleanup deterministic, observable, and recoverable.
- Share policy and test definitions while isolating platform-specific adapters.
- Prefer supported Gecko APIs and documented preferences over fragile engine patches.

## 2. Proposed logical components

| Component | Responsibility | Constraint |
|---|---|---|
| Browser Shell | Window/activity lifecycle, tabs, navigation chrome, menus | Must not expose privileged APIs to page content |
| Tab & Session Manager | Tabs, browsing contexts, session lifecycle, close coordination | Define when a session is fully closed |
| Navigation Controller | URL/search interpretation, navigation state, redirects, errors | Validate schemes and safely route external protocols |
| Gecko Adapter | Wrap supported engine APIs/preferences behind Umbra interfaces | UI widgets do not depend directly on engine internals |
| Privacy Policy Service | Source of truth for isolation, retention, and exceptions | Fail closed when a new privilege decision cannot be resolved |
| Site Permission Manager | Prompts, grants, revocation, expiry | Least privilege and site/capability scope |
| Site Data Inventory | Reports categories and policy disposition where APIs permit | Distinguish observed state from estimates or unknowns |
| Cleanup Coordinator | Plans and executes cleanup; reports and retries safe pending work | Idempotent; logs must not leak browsing data |
| Exception Manager | Stores approved exceptions, scope, and expiry | Explicit consent and easy revocation |
| Privacy Dashboard | Displays effective policy, exceptions, and cleanup outcomes | Never promise more than the engine can guarantee |
| Settings & Persistence | Bookmarks, browser preferences, download configuration | Separate browser-owned state from site data |
| Diagnostics | Local diagnostics and test instrumentation | No URLs, cookies, tokens, or page contents by default |
| Platform Adapter | OS integration, file picker, downloads, notifications, lifecycle hooks | Keep platform-specific code isolated |

## 3. Core flows

### Navigation

1. The shell receives a URL or search query.
2. The navigation controller validates and normalises the input.
3. The policy service resolves isolation and permission policy.
4. The Gecko adapter creates or navigates the appropriate context.
5. The shell reflects navigation state without granting page content access to privileged browser APIs.

### Permission or compatibility exception

1. Gecko or a browser subsystem reports a permission or compatibility need.
2. The manager identifies origin, capability, and required scope.
3. The policy service decides whether to allow, deny, or ask the user.
4. The UI explains the consequence and offers a narrow, revocable option.
5. The decision is stored with scope, creation time, and expiry where applicable.
6. The dashboard displays the effective decision and supports revocation.

### Browser close and cleanup

1. The shell begins shutdown and stops new navigation.
2. The session manager coordinates tabs, downloads, and active contexts.
3. The cleanup coordinator builds a plan from the policy service.
4. Eligible cleanup operations run through supported engine APIs.
5. Each category is marked success, failure, unsupported, or unknown.
6. If interrupted, retain a safe pending-cleanup marker outside the data being cleaned.
7. On next startup, resume safe outstanding operations.
8. Report completion and limitations; never claim a full wipe when required categories failed.

## 4. Conceptual interfaces

These are design-level interfaces, not final code signatures. Final APIs depend on the selected Gecko versions and platform wrappers.

### PrivacyPolicyService

- getEffectivePolicy(context, origin, capability)
- requiresConsent(change)
- evaluateException(origin, capability, requestedScope)
- getUserVisibleExplanation(decision)

### ExceptionManager

- requestException(origin, capability, scope, duration)
- listExceptions()
- revokeException(exceptionId)
- expireExceptions(now)

### CleanupCoordinator

- planCleanup(reason)
- executeCleanup(plan)
- getCleanupStatus(runId)
- recoverPendingCleanup()

### SiteDataInventory

- getSupportedCategories()
- getDisposition(category, context)
- getCleanupEvidence(runId)

Unsupported or unobservable state must not be presented as confirmed absence.

## 5. Gecko and GeckoView feasibility mapping

This section is a research checklist, not a claim that every API exists on every platform.

- **Desktop Gecko:** investigate profile lifecycle, browsing contexts, site isolation, cookie policy, storage partitioning, permissions, cache and service-worker cleanup, shutdown observers, and browser automation.
- **Android GeckoView:** investigate runtime/session lifecycle, content permissions, supported settings/preferences, storage-clearing APIs, and Android activity/process shutdown behaviour.
- **Shared policy layer:** policy schema, exception model, cleanup plan, user-facing explanations, and platform-independent acceptance tests.
- **Platform adapters:** shell integration, file handling, downloads, external protocol handoff, and lifecycle events.

For every required capability, record its supported API/preference, minimum engine version, platform coverage, limitations, and a test of effective behaviour. Avoid undocumented preferences unless the risk is explicitly reviewed.

## 6. Privacy dashboard state model

Show at least:

- Effective isolation mode and whether enforcement is complete or partial.
- Current-site permission state.
- Active compatibility exceptions and expiry.
- Close-cleanup policy.
- Last cleanup result, including failed or unknown categories.
- Controls to inspect and revoke exceptions.

Use distinct states for enabled, disabled, exception active, unsupported, pending, failed, and unknown. Never collapse unknown or failed into “protected.”

## 7. Failure handling

- Policy lookup failure: do not grant a new privilege by default.
- Cleanup category failure: continue independent operations and report incomplete cleanup.
- Crash during cleanup: recover on next launch where safe and idempotent.
- Expired exception: stop applying it and restore the baseline policy.
- Unsupported capability: disclose the limitation in the dashboard and test report.
- Corrupt exception data: ignore unsafe grants and notify the user if behaviour changes.

## 8. Test seams

Provide test injection for clock/time, supported storage categories, cleanup success/failure, shutdown/crash lifecycle, permission decisions, exception expiry, and dashboard status presentation.

## 9. Open architecture decisions

1. Confirm language, build system, and whether to extend an existing Gecko-based shell or create a new one.
2. Pin supported Gecko/GeckoView version ranges.
3. Identify APIs for each required storage category and lifecycle hook.
4. Define profile/session semantics, especially cleanup across multiple windows.
5. Finalise exception schema and persistence.
6. Choose the first vertical slice and CI platforms.

## 10. Acceptance criteria

- Every privacy requirement maps to components and tests.
- UI components do not independently decide storage policy.
- Every cleanup category has a supported API, documented limitation, or explicit exclusion.
- Failure and unknown states are visible and testable.
- Platform-specific lifecycle behaviour cannot silently bypass cleanup.
