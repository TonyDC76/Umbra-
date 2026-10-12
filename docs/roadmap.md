# Project Umbra — Roadmap

**Status:** Proposed sequencing; review before implementation commitments

## Phase 0 — Repository and product baseline

- [x] Establish repository and default branch.
- [x] Record initial privacy/site-storage policy decisions.
- [x] Add initial browser requirements baseline.
- [x] Draft component design and identify API research gaps.
- [ ] Add decision-record conventions.
- [ ] Confirm the application shell and build system.

## Phase 1 — Engine and platform feasibility

- [ ] Compare existing Gecko-based browser-shell options with building a new shell.
- [ ] Confirm supported Gecko/GeckoView versions and licence obligations.
- [ ] Build minimal launchable prototypes for Windows, macOS, Linux, and Android.
- [ ] Map each privacy requirement to supported APIs/preferences on each platform.
- [ ] Document gaps, risks, and platform-specific compromises.
- [ ] Establish automated build and test workflows.

**Exit criteria:** a reviewed feasibility report with an implementation path, version baseline, and evidence for core privacy controls.

## Phase 2 — Minimal browser shell

- [ ] Navigation and address/search input.
- [ ] Back, forward, reload/stop, loading, and error states.
- [ ] Tabs and session lifecycle.
- [ ] Basic menu and settings entry point.
- [ ] Safe external protocol and download handling.
- [ ] Accessibility and keyboard/touch baseline.

**Exit criteria:** a minimal browser navigates common sites on all in-scope platforms without bypassing browser/content security boundaries.

## Phase 3 — Privacy policy foundation

- [ ] Implement central privacy policy service.
- [ ] Configure and verify strict isolation and storage partitioning.
- [ ] Implement site permission inventory and revocation.
- [ ] Define compatibility exception schema and consent flow.
- [ ] Add privacy dashboard status model.
- [ ] Test defaults, overrides, expiry, and failure states.

**Exit criteria:** defaults and exceptions are visible, scoped, and verified by tests on each platform.

## Phase 4 — Close cleanup and recovery

- [ ] Build a storage-category capability matrix.
- [ ] Implement cleanup planning and execution on close.
- [ ] Handle active tabs, multiple windows/sessions, downloads, and shutdown ordering.
- [ ] Implement safe recovery after interruption.
- [ ] Report per-category success, failure, unsupported, or unknown status.
- [ ] Test cookies, local storage, IndexedDB, caches, service workers, and relevant browser-managed state where supported.

**Exit criteria:** cleanup is repeatable and tested; UI accurately reports limits and failures.

## Phase 5 — Compatibility and user experience

- [ ] Add privacy prompts with plain-language trade-offs.
- [ ] Add temporary, scoped exception choices where supported.
- [ ] Add dashboard inspection and revocation.
- [ ] Test sign-in, embedded content, media, and web-app workflows.
- [ ] Avoid asking users to weaken privacy without evidence.

**Exit criteria:** compatibility workflows do not silently weaken defaults and remain understandable to non-expert users.

## Phase 6 — Hardening and release readiness

- [ ] Threat model and security review.
- [ ] Cross-platform regression and privacy test suite.
- [ ] Performance and memory profiling.
- [ ] Accessibility review.
- [ ] Dependency and licence review.
- [ ] Reproducible release build and update strategy.
- [ ] Document known limitations and release criteria.

**Exit criteria:** release-blocking security/privacy tests pass and remaining limitations are documented.

## Priority rule

Privacy correctness and verifiable behaviour take precedence over feature breadth. Do not mark a phase complete based only on UI appearance or configuration values; require tests or documented evidence of effective behaviour.
