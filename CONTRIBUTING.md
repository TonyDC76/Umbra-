# Contributing to Project Umbra

Umbra is a privacy-focused cross-platform browser.

## Working principles

- Prefer small, reviewable changes with a clear purpose.
- Keep privacy decisions centralised and explicit.
- Do not weaken privacy defaults to solve compatibility issues without a documented decision and user-consent design.
- Never log cookies, authentication tokens, page contents, or unnecessary browsing data.
- Do not claim a privacy control works until its effective behaviour has been tested.
- Keep platform-specific code behind a clear adapter where practical.

## Before changing code

1. Read the relevant requirements and component-design documents.
2. Identify affected platforms and privacy/security boundaries.
3. Add or update acceptance tests.
4. Record material architectural or policy decisions in a decision record.
5. State assumptions and known limitations in the pull request.

## Pull request checklist

- [ ] The change has a clear problem statement and scope.
- [ ] Requirements and architecture documentation are updated where needed.
- [ ] Tests cover expected behaviour and important failure cases.
- [ ] Privacy/security implications have been considered.
- [ ] No secrets or unnecessary browsing data are included in logs or fixtures.
- [ ] Platform differences and unsupported behaviour are documented.
- [ ] User-facing privacy wording accurately describes the behaviour.

## Decision records

Use docs/decisions/ for decisions that materially affect architecture, privacy, security, platform support, or data retention. Each record should include context, decision, alternatives considered, consequences, and verification requirements.

## Scope

Current target platforms are Windows, macOS, Linux, and Android. iOS is outside the current scope.
