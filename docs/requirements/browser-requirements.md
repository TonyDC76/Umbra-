# Project Umbra — Browser Requirements

**Status:** Initial baseline for review  
**Platforms:** Windows, macOS, Linux, Android  
**Engine direction:** Gecko on desktop; GeckoView on Android  
**Out of scope:** iOS

## 1. Purpose and principles

Umbra is a privacy-focused, cross-platform web browser. Privacy protections should be understandable and enabled by default without making ordinary browsing unnecessarily difficult.

1. Privacy by default.
2. Explain privacy and compatibility trade-offs before consequential changes.
3. Make session and cleanup behaviour predictable.
4. Keep exceptions narrow, visible, and revocable.
5. Maintain consistent policy across platforms while documenting platform differences.
6. Verify behaviour through tests, not just configuration values.

## 2. Supported platforms

- Windows desktop
- macOS desktop
- Linux desktop
- Android

iOS is excluded from the current project scope.

## 3. Privacy and site storage baseline

**Requirement ID:** UMBRA-PRIV-STORAGE-001  
**Version:** 1.0

### 3.1 Isolation

- Strict site-data isolation is the default policy.
- State belonging to one site must not be exposed to unrelated sites through shared browser storage.
- Enable the strongest compatible storage partitioning supported by the selected engine and approved project policy.
- Account for first-party and third-party storage, including embedded content.
- A compatibility exception must not silently weaken the global default.

### 3.2 Data categories

The implementation must account for the following where supported and controllable:

- HTTP cookies, including session and persistent cookies
- localStorage and sessionStorage
- IndexedDB
- Cache API and site-owned web caches
- Service worker registrations and associated data
- HTTP/network caches that may retain site-derived information
- Site permissions and settings
- Authentication state and tokens stored by web content
- Browsing history and download history, according to separately defined browser-data policy

Clearly distinguish site-owned data from browser-owned settings and operating-system data. Do not promise deletion of data Umbra cannot reliably control.

### 3.3 Cleanup on browser close

- On normal browser close, clear eligible site data according to the approved policy.
- Coordinate shutdown and cleanup to avoid partial writes and avoidable corruption.
- Explain what is cleared, retained, unsupported, or unknown.
- Detect interrupted cleanup on the next startup and safely resume it where possible.
- Do not report cleanup as successful until the relevant operation completes; disclose failures and limitations.
- Test normal close, crash recovery, restart, and multiple-window/session cases.

### 3.4 Exceptions and compatibility

- Ask before enabling an exception to the default privacy policy.
- Explain the affected site, data category/capability, reason, privacy trade-off, scope, and duration.
- Scope exceptions to the minimum site and capability required.
- Make exceptions visible in settings and the privacy dashboard and easy to revoke.
- Never turn a transient failure into a permanent exception without explicit approval.
- Prefer temporary exceptions when technically feasible.

### 3.5 Transparency

- Users can inspect effective site-data policy and exception status.
- Distinguish data scheduled for deletion from data retained by an exception or technical limitation.
- Do not use vague claims such as “protected” when the effective state is partial, failed, or unknown.

## 4. Browser UI requirements

- Provide back, forward, reload/stop, address/search input, and tab controls.
- Provide a menu/dashboard entry point for privacy status, permissions, exceptions, downloads, history, and settings.
- Make privacy controls available both for the current site and in global settings.
- Explain consequential privacy changes before applying them.
- Support desktop and Android form factors, including keyboard navigation on desktop and accessible touch controls on Android.

## 5. Functional and security requirements

- Support URL navigation and search queries, multiple tabs, navigation state, and visible error feedback.
- Site permissions must be inspectable and revocable.
- Treat web content as untrusted and preserve the engine's browser/content privilege boundaries.
- Handle external protocols and downloads safely, with clear user intent.
- Do not write secrets, cookies, authentication tokens, page contents, or unnecessary browsing data to diagnostic logs by default.
- Give core controls accessible names and state announcements; do not rely on colour alone.

## 6. Storage baseline acceptance criteria

1. Default isolation is enabled on each supported platform.
2. Site storage is not unintentionally shared with unrelated sites.
3. Each in-scope storage category has a documented cleanup disposition.
4. Eligible data is cleared after normal browser close.
5. Interrupted cleanup is detected and safely recovered where possible.
6. Exceptions are never enabled silently.
7. Exceptions are scoped, visible, and revocable.
8. UI text accurately describes cleanup results and limitations.
9. Tests cover cookies, local storage, IndexedDB, caches, service workers, and embedded/third-party storage where supported.

## 7. Open decisions

- Exact Gecko preferences and APIs for isolation and partitioning.
- Definition of browser close when downloads, background tasks, multiple windows, or sessions remain active.
- Which categories are always cleared, optionally retained, or outside Umbra's control.
- Whether to support a separately retained profile or persistent site exception.
- Separate policy for passwords, bookmarks, downloads, crash reports, and browser settings.
- Exact exception wording, duration choices, and expiration behaviour.

## 8. Change control

Changes to requirements should record rationale, compatibility impact, test impact, and corresponding updates to component design and test plans. A configured preference alone is not proof of effective behaviour.
