# Known issues and limitations — Juno v0.5 Beta

Release `0.5.0-rc.1` · 2026-11-15 · Windows 11 x64 · Unsigned · Manual updates

This page lists what is currently known about **Juno v0.5 Beta**. It is
versioned: each item names the versions it affects, and resolved items say which
release fixed them. The same records are published as structured data for the
website at
[`support/v0.5.0-rc.1/known-issues.json`](support/v0.5.0-rc.1/known-issues.json),
so the site and this page cannot disagree.

Older releases keep their own documentation:
[v0.4.2 known issues](support/v0.4.2/KNOWN_ISSUES.md) ·
[v0.4.2 release](https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.2).

A listed limitation is a known boundary, not a promise that the area is
finished. Nothing here is a security advisory; see [SECURITY.md](SECURITY.md) for
responsible disclosure.

## Open issues

### `conversation-load-unavailable` — A carried-over conversation can fail to load

- **Affects:** `0.5.0-rc.1`
- **Status:** open · **Severity:** medium
- **What happens:** on a profile upgraded from an earlier beta — especially one
  restored from a backup — a companion can remember a conversation that is no
  longer attached to it. Juno then shows *“Your workspace is unavailable. Check
  the server connection in Advanced settings, then retry.”* and that transcript
  does not load.
- **Impact:** the affected conversation cannot be opened from that companion.
  The conversation is still stored in your profile; it is not deleted. Other
  companions and new conversations are unaffected.
- **Workaround:** none verified yet. Report it with your version if it blocks
  work; keep a profile backup.

## Limitations

1. **`windows-11-x64-only` — Windows 11 x64 is the only qualified platform.**
   Windows 10, ARM64, 32-bit Windows, macOS and Linux are not qualified for this
   beta.
2. **`unsigned-installer` — the installer is unsigned.** No Authenticode
   publisher identity and no SmartScreen reputation. Windows may warn or block.
   Verify the published SHA-256; do not disable Windows security controls.
3. **`manual-updates` — updates are manual.** Juno can announce a signed release
   and open its download page, but it never downloads or runs an installer for
   you.
4. **`no-in-place-downgrade` — an older build may not read v0.5 data.** Restore a
   pre-upgrade backup into a fresh profile instead of pointing an older installer
   at upgraded data.
5. **`provider-access` — external providers need your own access.** Accounts,
   subscriptions, network access and quota are required; catalogues, availability
   and billing are controlled by the provider.
6. **`chatgpt-models-account-scoped` — ChatGPT-plan models are account-scoped.**
   The list comes from the connected account and can be empty or change. A saved
   model that is no longer offered is reported, never silently replaced.
7. **`code-requires-omp` — Code work needs the external OMP runtime.** Juno
   bundles its Code coordinator (Boreal), the Ariadne verifier and the Codex
   runtime, but not OMP, and it cannot reuse every desktop provider login for
   Code.
8. **`no-workspace-spend-cap` — there is no enforceable workspace-wide spending
   cap.** Per-task ceilings and refusals for unpriced workers still apply.
9. **`ariadne-scope` — Ariadne verification is scoped.** It verifies
   owner-declared checks and the Code revision it is given, not every model
   statement or side effect.
10. **`read-only-code-scope` — read-only Code observes the project copy it was
    given.** Tool-owned trees (dependencies, build output, version-control
    metadata and caches) are excluded from the comparison, a project containing a
    link or reparse point is refused before it is copied, and changes another
    program makes to the project during the run are not reported.
11. **`update-notice-not-connected` — in-app update notices are not yet pointed
    at this release.** The signed feed still describes the previous beta; until
    it is republished, the releases page is authoritative.
12. **`remote-paired-unqualified` — modeled actions are desktop-scoped.** The
    paired-client authorization defect is fixed, but a live paired-device
    mutation run was not part of this qualification.
13. **`accessibility-walkthrough-partial` — the screen-reader walkthrough is
    partial.** Keyboard navigation, focus, contrast, scaling, forced colours and
    reduced motion are covered; a full NVDA/Narrator session was not completed.
14. **`optional-runtimes-download` — some Windows integrations are optional
    downloads.** The browser engine, Android platform tools and cloudflared are
    installed on request from Settings; a download that is still running is not
    treated as installed.

## Resolved in 0.5.0-rc.1

1. **`read-only-code-without-target`** — a read-only Code question with no file
   target or command was refused for having no acceptance check. It now derives a
   no-change criterion and passes only when nothing changed. *Fixed in
   `0.5.0-rc.1`.*
2. **`value-change-read-as-investigation`** — a request such as “Set the exported
   value to 2” was routed as an investigation, so its correct edit failed. It is
   now recognized as a mutating request. *Fixed in `0.5.0-rc.1`.*
3. **`credential-rejection-shown-as-catalog-outage`** — a rejected credential
   found during catalogue discovery looked like a catalog outage. It is now
   reported as an authentication problem with the action to take. *Fixed in
   `0.5.0-rc.1`.*
4. **`update-announcement-no-release-page`** — an update announcement could not
   name its own download page. A signed announcement may now carry its own
   validated HTTPS release page, with the build’s page as fallback. *Fixed in
   `0.5.0-rc.1`.*

## Reporting

Use [FEEDBACK.md](FEEDBACK.md) for bugs and feature requests, and
[SECURITY.md](SECURITY.md) for security problems. Do not post credentials,
private file paths or personal content in a public issue.
