# Changelog

## v0.5.1 Beta — 2026-11-16

A security and reliability maintenance release for the v0.5 public beta.

### Security

- Fixed isolation of local Juno data between separate Windows user accounts.
- Existing v0.5.0 users should upgrade manually.

### Reliability

- Fixed OpenCode managed installation and model discovery (`@opencode/cli` 2.x).
- Kept provider cards and model choices stable across restart.
- Fixed ChatGPT single-model save, restart state and quota-error classification.
- Rejected reasoning-only responses as final answers.
- Recovered safely from stale local conversation pointers.
- Added clean port-conflict fallback and restart-safe startup.

### Usability

- Clearer onboarding and provider setup states.
- Improved Settings, provider rows and companion selection.
- Smoother right-side workspace panel; spacing and accessibility corrections.

### Distribution

- Windows 11 x64, unsigned installer, manual updates.
- Signed update feed unchanged at `0.4.2-rc.3`; no in-app v0.5.1 announcement.
- SHA-256: `A4375A29888956BE688ADB1BC714A10D2F84B04BCB349676ABCA9B0CED3B09BF`.

## v0.5.0 Beta — 2026-11-15

Unified companion-first workspace, Code and Missions, provider setup, local-first storage and
optional runtime downloads. See the v0.5.0 release notes and support archive.
