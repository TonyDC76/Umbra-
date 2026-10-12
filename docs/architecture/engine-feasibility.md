# Project Umbra — Engine Feasibility Notes

**Status:** Preliminary research; desktop architecture remains undecided  
**Reviewed:** 2026-10-13  
**Scope:** Gecko/GeckoView across Windows, macOS, Linux, and Android

## Executive summary

The Gecko direction is well supported on Android through GeckoView, which Mozilla documents as an embeddable Gecko library suitable for browser development. The desktop side needs a separate feasibility decision: do not assume GeckoView is a cross-platform desktop embedding API. Before choosing a desktop implementation, compare building on Firefox's desktop codebase with any supported embedding approach and quantify maintenance/build costs.

**Recommendation:** Keep Gecko/GeckoView as the engine direction to investigate, but do not lock the desktop implementation until a small technical spike proves the path and privacy controls.

## Findings

### Android

Mozilla's official GeckoView documentation describes GeckoView as a standalone library for embedding Gecko in Android apps and explicitly points browser builders toward Android Components. Its documented integration uses GeckoRuntime, GeckoSession, and GeckoView. This provides a clear starting point for an Android prototype.

Sources:
- Mozilla GeckoView documentation: https://firefox-source-docs.mozilla.org/mobile/android/geckoview/index.html
- GeckoView quick start: https://mozilla.github.io/geckoview/consumer/docs/geckoview-quick-start
- GeckoView architecture: https://firefox-source-docs.mozilla.org/mobile/android/geckoview/contributor/geckoview-architecture.html

### Desktop

The reviewed GeckoView material is specifically about Android. It does not establish a supported, equivalent GeckoView embedding API for Windows, macOS, and Linux. Desktop implementation therefore needs its own technical investigation; options may include building on the Firefox desktop codebase or another supported route if one can be demonstrated.

The cost is not just rendering a web page. Umbra needs browser chrome, tab/session lifecycle, permissions, storage policy, cleanup, updates, security fixes, packaging, and tests. A desktop approach that only embeds a rendering widget may not expose enough supported control to satisfy the privacy requirements.

Official Mozilla starting point for desktop-codebase investigation:
- Firefox source documentation: https://firefox-source-docs.mozilla.org/

## Feasibility spike

Run a short, evidence-driven spike before committing to a full implementation:

1. **Android proof:** build a minimal GeckoView app that opens a GeckoRuntime, creates a GeckoSession, and loads a page.
2. **Desktop proof:** identify the maintained desktop build path and produce a minimal browser build or a documented blocker for each of Windows, macOS, and Linux.
3. **Privacy API map:** for each candidate, verify access to cookies, storage partitioning, permissions, service workers, caches, profile lifecycle, and shutdown cleanup.
4. **Build/maintenance estimate:** record toolchains, hardware/storage requirements, build times, release cadence, patch burden, and security-update workflow.
5. **Licence review:** identify relevant engine and dependency licences and obligations before distribution.
6. **Decision review:** compare options against privacy-control coverage, platform coverage, compatibility, build/maintenance cost, and long-term security updateability.

## Required output

Create a comparison table with one row per candidate and platform, recording:

- Supported integration/build route and source documentation
- Engine versioning and security update mechanism
- Access to each required privacy control
- API stability and reliance on undocumented interfaces
- Development and CI prerequisites
- Build/package size and update implications
- Known gaps, risks, and confidence level

## Decision gate

Do not start broad browser feature implementation until:

- A viable desktop path is demonstrated or its blockers are accepted explicitly.
- Android GeckoView integration is demonstrated.
- The core isolation and cleanup controls have a plausible, testable implementation path on every target platform.
- The maintenance burden is understood well enough to support timely security updates.

## Source notes

This is a preliminary documentation review, not a completed prototype or a claim that all privacy requirements can already be met. Re-check the official docs and current supported APIs during implementation because engine APIs and release practices evolve.
