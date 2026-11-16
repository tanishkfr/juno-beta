# Known issues and limitations — Juno v0.5.1 Beta

Release `0.5.1-rc.1` · 2026-11-16 · Windows 11 x64 · Unsigned · Manual updates

This page lists the public limitations for **Juno v0.5.1 Beta**. The same records are published
as structured data at
[`support/v0.5.1-rc.1/known-issues.json`](support/v0.5.1-rc.1/known-issues.json), so the website
and this page cannot disagree. Older releases keep their own documentation:
[v0.5.0](support/v0.5.0-rc.1/known-issues.json) and
[v0.4.2](support/v0.4.2/KNOWN_ISSUES.md).

A listed limitation is a known boundary, not a promise that the area is finished. Nothing here is
a security advisory; see [SECURITY.md](SECURITY.md) for responsible disclosure.

## Security

### `cross-user-loopback-reads` — local data isolation between Windows accounts (resolved)

- **Affected:** `0.5.0-rc.1`
- **Fixed in:** `0.5.1-rc.1`
- **What changed:** earlier v0.5 builds could expose some local Juno data to another Windows user
  on the same PC under specific local conditions. v0.5.1 requires the packaged desktop
  capability, or a paired session, for local data routes. Health and static identity routes remain
  public. Existing v0.5.0 users should upgrade manually.

## Open limitations

1. **`windows-11-x64-only`** — Windows 11 x64 is the only qualified platform. Windows 10, ARM64,
   32-bit Windows, macOS and Linux are not qualified.
2. **`unsigned-installer`** — no Authenticode publisher identity or SmartScreen reputation.
   Verify the published SHA-256; do not disable Windows security controls.
3. **`manual-updates`** — Juno never downloads or runs an installer for you. The signed feed still
   describes `0.4.2-rc.3`; v0.5.1 is a manual download and no in-app announcement is expected.
4. **`no-in-place-downgrade`** — an older build may not read v0.5.1 data. Restore a pre-upgrade
   backup into a fresh profile instead.
5. **`provider-access`** — provider accounts, subscriptions, network access and quota are
   required. Catalogues, availability and billing are controlled by the provider.
6. **`provider-quota`** — provider quota and rate limits are external. Juno reports the condition
   it observed; it cannot reset or bypass a provider quota.
7. **`chatgpt-models-account-scoped`** — the ChatGPT-plan model list comes from the connected
   account and can be empty or change. A saved model that is no longer offered is reported, never
   silently replaced.
8. **`code-requires-omp`** — Code execution needs the external OMP runtime. Boreal, Ariadne and
   Codex are bundled; OMP is not.
9. **`no-workspace-spend-cap`** — per-task ceilings apply, but Juno cannot enforce a hard
   workspace-wide cap across every external provider route.
10. **`ariadne-scope`** — Ariadne verifies owner-declared checks and the Code revision it is given;
    it does not prove every model statement or tool side effect.
11. **`read-only-code-scope`** — read-only Code observes the project copy it was given; changes
    made by another program during the run are outside that copy.
12. **`remote-paired-unqualified`** — the paired-device authorization suites pass, but a live
    paired-device mutation run was not part of this qualification. Keep modeled actions in the
    desktop app.
13. **`accessibility-walkthrough-partial`** — keyboard, focus, contrast, text scaling, forced
    colours and reduced motion are covered; a full NVDA/Narrator speech-output session was not
    completed for this release.
14. **`optional-runtimes-download`** — the browser engine, Android platform tools, cloudflared and
    Whisper are optional downloads; a download still running is not treated as installed.
15. **`clean-vm-not-run`** — a clean Windows 11 VM install/first run was not part of this
    qualification. The interactive owner-session install passed.

## Resolved in v0.5.1

- `conversation-load-unavailable` — a stale local conversation pointer no longer strands the
  workspace; the companion returns to a valid conversation and stored messages are kept.
- `chatgpt-quota-shown-as-auth` — provider usage-limit prose is no longer shown as a connection
  failure.
- `reasoning-only-answer` — a response with reasoning but no answer text now fails the turn
  instead of being shown as the reply.
- `opencode-managed-install` — the managed runtime uses `@opencode/cli` 2.x and refreshes models
  without restarting the app.
- `provider-cards-disappear` — provider cards remain present while the optional catalogue loads
  and after restart.
- `chatgpt-single-model-save` — a sole eligible model saves correctly.
