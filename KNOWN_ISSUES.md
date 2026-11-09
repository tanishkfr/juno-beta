# Known issues and limitations — Juno v0.4.0 Beta

Release `0.4.0` · 2026-11-10 · Windows 11 x64

This is the current limitation list for **Juno v0.4.0 Beta — Intelligence &
Efficiency**. A listed limitation is a known boundary, not a claim that the area
is production-ready.

## Release and installation

1. **Windows 11 x64 only.** Windows 10, macOS, Linux, ARM64 and 32-bit Windows
   are not qualified for this Beta.
2. **Unsigned installer.** The installer has no Authenticode signature. Windows
   may show Unknown Publisher or SmartScreen, and some managed PCs may block
   it. Verify the published SHA-256 before running it. Do not disable Windows
   security controls.
3. **Manual updates.** Juno does not download or run installers. Installation
   and updates are manual for this Beta.
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
8. **The signed automatic-update bridge from the old `1.0.0-rc` line is not
   qualified.** Do not wait for an automatic update. Download the installer
   manually.
9. **Signed metadata is announcement-only.** Juno may check Ed25519-signed
   release metadata and show release notes. `electron-updater` has no live
   automatic-install feed, and Juno never runs an installer for you.
10. **No general downgrade support.** Running an older installer manually is
    possible, but data written by a newer build may not be understood by the
    older one. Back up local data before rolling back.

## Provider and network

11. **Provider accounts, subscriptions, quotas and network access are
    required** for external models. Juno does not supply provider capacity.
12. **Model availability can change independently of Juno.** A provider may
    retire, rename or restrict a model. An explicit stale pin is refused rather
    than silently replaced.
13. **Command Code credentials may need replacement.** In the final release
    smoke, one Command Code credential was rejected by the provider while the
    Codex route worked. This is an account/credential state, not a Juno
    installer failure. Replace the credential in provider settings.

## Capability qualification

14. **Council is bounded evidence.** The economical and balanced presets were
    exercised live with a planner and an independent reviewer. Not every
    provider or custom role combination was re-run.
15. **Browser and computer control are bounded.** The packaged browser engine
    and CUA driver were exercised directly against real runtimes. A
    model-driven multi-application computer task was not re-run for this
    release.
16. **Code Mode uses the bundled Boreal/OMP runtime.** It needs provider
    authentication configured there; Juno cannot reuse every desktop provider
    login for it.
17. **Screen-reader acceptance is partial.** Keyboard navigation, visible focus,
    contrast, zoom, forced colours and reduced motion were checked. A real
    NVDA/Narrator speech-output session was not completed.
18. **Voice dictation is bounded.** Local Windows speech output and local
    Whisper transcription were tested on one machine. Accuracy in noisy rooms
    and long sessions is not guaranteed.
19. **No enforceable workspace-wide spending hard cap.** Unpriced external Code
    workers are refused under a task ceiling unless explicitly allowed.
20. **Some inherited surfaces are visible but not qualified for this Beta.**
    Teams, organization, Cloud, mobile pairing, backups and routines exist in
    the codebase from earlier work. Do not treat every visible control as a
    tested public-beta capability.
21. **The installer was qualified on one Windows 11 machine.** A fresh
    independent Windows profile or disposable VM was not available for this
    pass. Install, upgrade, uninstall/reinstall, rollback and data preservation
    were exercised on the owner's Windows 11 profile with verified backups.

## Performance

22. **Reply time is provider-bound.** The earlier CommandCode/DeepSeek
    qualification measured 39–44 ms of Juno dispatch and 2.4–3.0 seconds for a
    short warm reply. The final packaged Codex smoke measured about 5–7 seconds
    end to end. These are measurements, not guarantees.
23. **Browser and computer first use depends on the runtime.** First browser
    open was about 1.5–1.9 seconds against a loopback fixture; first CUA screen
    query was under 1 second. Real sites and real applications add their own
    latency.

## Reporting a problem

Use **Settings > Help & feedback > Report a bug**, then **Open Email Draft**.
Include the Juno version, Windows version, feature, expected and actual
behavior, steps to reproduce and whether it repeats. Remove API keys, tokens,
cookies, private file paths and personal documents before sending.

You can also open an issue at
<https://github.com/tanishkfr/juno-beta/issues>.
