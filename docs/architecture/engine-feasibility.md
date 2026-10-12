# Project Umbra — Engine Feasibility Notes

**Status:** Preliminary research; Windows implementation path remains undecided  
**Reviewed:** 2026-10-13  
**Initial scope:** Windows desktop  
**Long-term scope:** macOS, Linux, and Android

## Executive summary

The immediate goal is to prove a maintainable Windows browser engine/build path and the core privacy controls. macOS, Linux, and Android remain long-term targets, but their prototypes should not block the initial Windows feasibility work.

GeckoView is documented as an Android embedding library. Do not assume it is a desktop embedding API. For Windows, compare a maintained Firefox desktop-codebase route with any supported alternative and quantify maintenance/build costs. Keep future platform ports as independent feasibility decisions.

**Recommendation:** Run a Windows-first spike. Do not lock the implementation until it demonstrates navigation, a maintainable security-update path, and access to the required privacy controls.

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

## Windows-first feasibility spike

Complete this spike before building the full interface:

1. **Build path:** identify the maintained Windows engine/build route and build or launch a minimal browser proof.
2. **Navigation proof:** load ordinary HTTPS pages and verify basic navigation and error handling.
3. **Privacy API map:** verify access to cookies, storage partitioning, permissions, service workers, caches, profile lifecycle, and shutdown cleanup.
4. **Build/maintenance estimate:** record toolchains, hardware/storage requirements, build times, release cadence, patch burden, and security-update workflow.
5. **Licence review:** identify relevant engine and dependency licences and obligations before distribution.
6. **Decision review:** assess privacy-control coverage, compatibility, build/maintenance cost, and timely security updates.

## Future platform gates

After the Windows approach is viable, evaluate each future target independently:

- **Linux and macOS:** demonstrate a maintained desktop build/integration route and map the same privacy controls.
- **Android:** build a minimal GeckoView app using GeckoRuntime and GeckoSession, then verify storage and lifecycle controls.

Do not make future-platform prototypes a prerequisite for the first Windows milestone.

## Required output

Create a Windows candidate comparison first, then extend it as future platforms are evaluated. Record:

- Supported integration/build route and source documentation
- Engine versioning and security update mechanism
- Access to each required privacy control
- API stability and reliance on undocumented interfaces
- Development and CI prerequisites
- Build/package size and update implications
- Known gaps, risks, and confidence level

## Decision gate

Do not start broad browser feature implementation until:

- A viable Windows path is demonstrated or its blockers are accepted explicitly.
- The core isolation and cleanup controls have a plausible, testable Windows implementation path.
- The maintenance burden is understood well enough to support timely security updates.
- Future macOS, Linux, and Android work remains documented but does not block this initial decision.

## Source notes

This is a preliminary documentation review, not a completed prototype or a claim that all privacy requirements can already be met. Re-check the official docs and current supported APIs during implementation because engine APIs and release practices evolve.
