# Project Umbra — Roadmap

**Status:** Windows-first delivery plan; macOS, Linux, and Android remain long-term targets.

## Phase 0 — Repository and product baseline

- [x] Establish repository and default branch.
- [x] Record initial privacy/site-storage policy decisions.
- [x] Add initial browser requirements baseline.
- [x] Draft component design and identify engine research gaps.
- [x] Record Windows-first scope while retaining future platform goals.
- [ ] Add decision-record conventions.

## Phase 1 — Windows engine and privacy feasibility

- [ ] Compare viable Windows engine/build routes, including maintenance of the Firefox desktop codebase.
- [ ] Produce a minimal Windows build/launch/navigation proof.
- [ ] Map the required privacy controls to supported Windows engine APIs/preferences.
- [ ] Demonstrate a credible security update and rebuild workflow.
- [ ] Review licences, toolchains, storage/build requirements, and maintenance cost.
- [ ] Record unresolved gaps and make an explicit engine decision.

**Exit criteria:** a viable Windows path is demonstrated, privacy controls have a testable implementation route, and ongoing security maintenance is realistic.

## Phase 2 — Minimal Windows browser shell

- [ ] Navigation and address/search input.
- [ ] Back, forward, reload/stop, loading, and error states.
- [ ] Tabs and session lifecycle.
- [ ] Basic menu and settings entry point.
- [ ] Safe external protocol and download handling.
- [ ] Keyboard accessibility and Windows integration baseline.

**Exit criteria:** a minimal Windows browser navigates common sites while preserving browser/content security boundaries.

## Phase 3 — Windows privacy foundation

- [ ] Implement central privacy policy service.
- [ ] Configure and verify strict isolation and storage partitioning.
- [ ] Implement site permission inventory and revocation.
- [ ] Define compatibility exception schema and consent flow.
- [ ] Add privacy dashboard status model.
- [ ] Test defaults, overrides, expiry, and failure states.

**Exit criteria:** privacy defaults and exceptions are visible, scoped, and verified by Windows tests.

## Phase 4 — Windows close cleanup and recovery

- [ ] Build a storage-category capability matrix for Windows.
- [ ] Implement cleanup planning and execution on close.
- [ ] Handle active tabs, multiple windows, downloads, and shutdown ordering.
- [ ] Implement safe recovery after interruption.
- [ ] Report per-category success, failure, unsupported, or unknown status.
- [ ] Test cookies, local storage, IndexedDB, caches, service workers, and relevant browser-managed state where supported.

**Exit criteria:** cleanup is repeatable and tested; the UI accurately reports limits and failures.

## Phase 5 — Windows compatibility and user experience

- [ ] Add privacy prompts with plain-language trade-offs.
- [ ] Add temporary, scoped exception choices where supported.
- [ ] Add dashboard inspection and revocation.
- [ ] Test sign-in, embedded content, media, and web-app workflows.
- [ ] Avoid asking users to weaken privacy without evidence.

**Exit criteria:** compatibility workflows do not silently weaken defaults and remain understandable to non-expert users.

## Phase 6 — Windows hardening and release readiness

- [ ] Threat model and security review.
- [ ] Windows regression and privacy test suite.
- [ ] Performance and memory profiling.
- [ ] Accessibility review.
- [ ] Dependency and licence review.
- [ ] Reproducible release build and update strategy.
- [ ] Document known limitations and release criteria.

**Exit criteria:** release-blocking security/privacy tests pass and remaining limitations are documented.

## Phase 7 — Future platform expansion

This phase begins after the Windows implementation path is proven and the Windows privacy baseline is stable enough to serve as a reference.

- [ ] Reassess shared architecture and identify required platform adapters.
- [ ] Evaluate Linux desktop engine/build integration.
- [ ] Evaluate macOS desktop engine/build integration.
- [ ] Evaluate Android integration, including GeckoView feasibility.
- [ ] Map every platform to the same privacy requirements and identify API gaps.
- [ ] Build and test one platform at a time, in a separately agreed priority order.
- [ ] Keep platform-specific limitations explicit; do not claim parity until tests pass.

**Exit criteria:** each added platform independently passes its engine feasibility gate and the applicable privacy, compatibility, and release tests.

## Cross-platform design rule

Do not over-engineer the initial Windows release for hypothetical portability. Instead, isolate OS-specific code where it is practical and low-cost, document assumptions, and keep privacy policy/data models testable independently. The long-term goal is Windows, macOS, Linux, and Android support; iOS is not currently planned.

## Priority rule

Privacy correctness, a maintainable engine, and timely security updates take precedence over feature breadth. Do not mark a phase complete based only on UI appearance or configuration values; require tests or documented evidence.
