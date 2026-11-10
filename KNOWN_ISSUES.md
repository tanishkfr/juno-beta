# Known issues and limitations — Juno v0.4.1 Beta

Release `0.4.1` · 2026-11-10 · Windows 11 x64

This is the current limitation list for **Juno v0.4.1 Beta — Unified Agent
Runtime**. A listed limitation is a known boundary, not a claim that the area is
production-ready.

## Release and installation

1. **Windows 11 x64 only.** Windows 10, macOS, Linux, ARM64 and 32-bit Windows
   are not qualified for this Beta.
2. **Unsigned installer.** The installer has no Authenticode signature. Windows
   may show Unknown Publisher or SmartScreen, and some managed PCs may block
   it. Verify the published SHA-256 before running it. Do not disable Windows
   security controls.
3. **Manual updates.** Juno does not download or run installers. Installation
   and updates are manual for this Beta. The signed automatic-installer upgrade
   path is not qualified.
4. **In-place upgrade only.** Juno uses the same application identity as earlier
   Beta builds. It upgrades an existing installation in place; it does not
   install side by side.
5. **Compact vs full.** The compact installer omits the browser engine and
   Whisper weights; both are optional, verified downloads. The full/offline
   variant includes them. External model providers still need internet access.
6. **Disk space.** About 1.05 GB installed for the compact build, about 1.50 GB
   for the full build, plus optional assets, projects and backups.

## Updates and signing

7. **No Authenticode publisher identity and no SmartScreen reputation.** SHA-256
   proves integrity, not who built the file.
8. **The signed automatic-installer upgrade path is not qualified.** Do not wait
   for an automatic update. Download the installer manually.
9. **Signed metadata is announcement-only.** Juno may check Ed25519-signed
   release metadata and show release notes. `electron-updater` has no live
   automatic-install feed, and Juno never downloads or runs an installer for
   you. The packaged `app-update.yml` uses the reserved host `updates.invalid`.
10. **No general downgrade support.** Running an older installer manually is
    possible, but data written by a newer build may not be understood by the
    older one. Back up local data before rolling back.
11. **Rollback rewrites schema metadata.** A v0.4.0 rollback records schema 5.
    All tables and rows remain readable, and reinstalling v0.4.1 restores schema
    7. Unrestricted rollback compatibility with future schema versions is not
    promised.

## Spending controls

12. **No enforceable workspace-wide spending hard cap.** A hard cap remains
    unenforceable across some external provider routes. Do not treat Juno as an
    absolute spending guarantee.
13. **Boreal internal worker iterations are not all bounded by Juno's
    model-call ceiling.** Juno authorizes and verifies the worker model and
    policy. Boreal's internal loop count is outside Juno's interception.
14. **Unpriced usage remains unknown.** Subscription-backed usage is often
    unpriced and is recorded as unknown, not zero. Unpriced external workers
    under a task ceiling remain refused unless explicitly allowed.

## Provider and network

15. **Provider accounts, subscriptions, quotas and network access are
    required** for external models. Juno does not supply provider capacity.
    Each provider has independent account, subscription, quota and network
    requirements.
16. **Model availability can change independently of Juno.** A provider may
    retire, rename or restrict a model. An explicit stale pin is refused rather
    than silently replaced.
17. **Command Code credentials may need replacement.** In an earlier release
    smoke, one Command Code credential was rejected by the provider while the
    Codex route worked. This is an account/credential state, not a Juno
    installer failure. Replace the credential in provider settings.

## Capability qualification

18. **Speech acceptance is partial.** Installed speech components and local
    Whisper transcription passed. The installed app reported its speech engine,
    microphone, Windows recognizers and on-device Whisper model ready, and the
    bundled Whisper engine transcribed a synthetic WAV exactly. **Live
    microphone recording was not exercised during final qualification**, so a
    human recording and cancellation-cleanup pass remain owner acceptance items.
19. **Browser close is model-dependent.** The installed browser task opened and
    read the page correctly and surfaced every approval. The tested model omitted
    a required `tabId` on its initial browser-close call. Juno reported the tool
    error honestly and the session was subsequently released with the shipped
    browser engine. This is not reported as a successful model-driven close.
20. **Computer-control qualification was a read-only probe.** The packaged
    embedded CUA host started and returned the real desktop size and window list.
    It was not a full model-driven click or multi-application interaction.
21. **No clean-room Windows VM.** Installation, upgrade, uninstall/reinstall,
    full/offline install and rollback were exercised on the owner's existing
    Windows 11 environment with verified backups, not on a fresh VM.
22. **The real installed full/offline variant was tested on the owner's
    existing Windows environment.** The compact and full installers share the
    same application code; the full variant adds the browser engine, Whisper
    model, accessibility resources and Boreal coordinator.
23. **Council is bounded evidence.** Planner, executor and reviewer roles were
    exercised live on the qualified route. Not every provider or custom role
    combination was re-run.
24. **Code Mode uses the bundled Boreal/OMP runtime.** It needs provider
    authentication configured there; Juno cannot reuse every desktop provider
    login for it.
25. **Screen-reader acceptance is partial.** Keyboard navigation, visible focus,
    contrast, zoom, forced colours and reduced motion were checked. A real
    NVDA/Narrator speech-output session was not completed.
26. **Some inherited surfaces are visible but not qualified for this Beta.**
    Teams, organization, Cloud, mobile pairing, backups and routines exist in
    the codebase from earlier work. Do not treat every visible control as a
    tested public-beta capability.

## Performance

27. **Reply time is provider-bound.** The final candidate measured warm short
    replies at about **2.29–2.92 seconds** on the tested route. These are
    measurements, not guarantees, and they do not imply that the underlying
    models became faster or smarter.
28. **Durable task overhead is small but present.** The qualification
    microbenchmark measured about **7.06 ms p50** and 12.57 ms p95 for the
    Juno-controlled task record. Provider and network latency dominate the
    visible reply time.

## Reporting a problem

Use **Settings > Help & feedback > Report a bug**, then **Open Email Draft**.
Include the Juno version, Windows version, feature, expected and actual
behavior, steps to reproduce and whether it repeats. Remove API keys, tokens,
cookies, private file paths and personal documents before sending.

You can also open an issue at
<https://github.com/tanishkfr/juno-beta/issues>.
