# Project Umbra

Umbra is a privacy-focused web browser, starting with a Windows desktop release and designed with a longer-term cross-platform goal.

## Delivery scope

- **Initial target:** Windows desktop only.
- **Long-term targets:** Windows, macOS, Linux, and Android.
- **Engine direction:** To be proven for Windows first; future desktop and Android implementations may require different integration paths.
- **iOS:** Outside the current plan.

The initial Windows focus is a sequencing decision, not a cancellation of the other operating systems. Shared privacy policy and browser logic should be separated from platform-specific integration where practical, so future ports remain possible without burdening the first release with unproven cross-platform work.

## Privacy baseline

Umbra's design direction is strict site-data isolation by default, clearing eligible site data when the browser closes, and asking users before enabling compatibility exceptions while explaining the trade-offs. These are requirements to validate, not claims of implemented behaviour.

## Project documents

- [Browser requirements](docs/requirements/browser-requirements.md)
- [Component design](docs/architecture/component-design.md)
- [Engine feasibility notes](docs/architecture/engine-feasibility.md)
- [Roadmap](docs/roadmap.md)
- [Scope decision record](docs/decisions/0001-windows-first.md)
- [Contribution guidelines](CONTRIBUTING.md)

## Status

The repository contains the initial product requirements and proposed architecture. The next milestone is to prove a maintainable Windows engine/build path and validate the core privacy controls before building the full browser interface. macOS, Linux, and Android remain explicit future targets.
