# ADR 0001: Windows-first initial release

- **Status:** Accepted
- **Date:** 2026-10-13

## Context

The original project scope targeted Windows, macOS, Linux, and Android from the outset. Proving the engine, privacy controls, lifecycle behaviour, packaging, and security-update path across all of these platforms at once would substantially increase initial complexity and risk.

## Decision

1. The initial implementation and first release target **Windows desktop only**.
2. The first engineering milestone is to prove a maintainable Windows engine/build path and validate the core privacy controls before broad browser UI implementation.
3. macOS, Linux, and Android remain explicit long-term targets. They are deferred, not cancelled.
4. Future platforms will be assessed and implemented through separate feasibility gates, each with a demonstrated engine integration path and tests for the required privacy behaviour.
5. Shared privacy policy and data models should be kept independent of OS integration where practical. Windows-specific code should use clear boundaries, but the first release must not be burdened with speculative abstractions that have no immediate value.
6. iOS remains outside the current plan.

## Consequences

### Benefits

- Reduces the initial engine, build, test, and release scope.
- Lets the project validate privacy assumptions on one platform before multiplying the work.
- Establishes a concrete implementation and test baseline for later ports.

### Costs and risks

- Cross-platform issues may be discovered later, potentially requiring refactoring.
- Windows-specific decisions can make future ports harder if their assumptions are not documented.
- A future platform may require a different engine integration path or may prove infeasible within the project's maintenance budget.

### Mitigations

- Keep privacy policy and cleanup decisions in shared, testable components where practical.
- Document platform assumptions and keep OS integration at explicit boundaries.
- Re-evaluate portability during architecture reviews rather than attempting to solve all future platform concerns upfront.
- Require each future platform to pass its own engine and privacy feasibility gates.

## Acceptance criteria

- README, requirements, architecture, and roadmap consistently identify Windows as the initial target.
- macOS, Linux, and Android remain recorded as future targets.
- The next milestone is a Windows engine/build and privacy-control proof, not full UI development.
