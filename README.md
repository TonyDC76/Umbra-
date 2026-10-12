# Project Umbra

Umbra is a privacy-focused, cross-platform web browser.

## Project scope

- **Platforms:** Windows, macOS, Linux, and Android
- **Engine direction:** Gecko on desktop and GeckoView on Android
- **iOS:** Out of scope for the current project

## Privacy baseline

Umbra's current design direction is strict site-data isolation by default, clearing eligible site data when the browser closes, and asking users before enabling compatibility exceptions while explaining the trade-offs. These are requirements to validate, not claims of implemented behaviour.

## Project documents

- [Browser requirements](docs/requirements/browser-requirements.md)
- [Component design](docs/architecture/component-design.md)
- [Roadmap](docs/roadmap.md)
- [Contribution guidelines](CONTRIBUTING.md)

## Status

The repository currently contains the initial product requirements and proposed architecture. The next major step is to validate the Gecko/GeckoView implementation path and confirm the exact APIs and limitations for privacy isolation and cleanup on each target platform.

