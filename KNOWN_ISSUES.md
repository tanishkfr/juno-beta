# Known Issues: Juno Beta 0.3 (Final)

Release `1.0.0-rc.18` · 2026-10-26 · Windows 11 x64

This is the current limitation list for Juno Beta 0.3 (Final). Older lists belong to earlier Beta releases and are not a description of rc.18.

The product is a private Beta. A limitation listed here is a known boundary, not a claim that the area is production-ready.

## Release and installation

1. **Windows only.** Windows 11 x64 is the supported platform. Windows 10, macOS and Linux are not qualified for this Beta.
2. **Unsigned installer.** Windows may show Unknown Publisher or SmartScreen. Verify the published SHA-256 before running the installer. No code-signing certificate is used for this Beta.
3. **rc.18 NSIS installation is not independently verified yet.** The published installer's size and SHA-256 match the release, and the extracted packaged application passed acceptance testing, but the rc.18 installer, first launch from the installed location and uninstaller have not been run in a fresh independent Windows environment. Report any installation failure with exact text.
4. **In-place upgrade only.** rc.18 uses the same Windows application identity as earlier Juno Beta builds. It upgrades an existing Beta installation in place; it does not install side by side.
5. **Private distribution.** Testers need a GitHub collaborator invitation to this repository. A copied release URL does not grant access.
6. **Installer size.** The installer is about 392 MB. Allow about 1 GB free for the application and generated work.

## Updates

7. **Automatic update discovery works.** Juno checks an Ed25519-signed HTTPS metadata feed after launch and every six hours. Settings > Updates shows the available version and the owner's notes. This was verified in the packaged application against the live feed.
8. **Installation is manual.** The installer is unsigned, so Juno never downloads, runs or silently installs an update. Open Beta releases leads to this release page; Verify downloaded installer checks a file against its checksum.
9. **Builds before rc.18 cannot discover updates.** rc.17 and earlier contain no feed or public key. Installing rc.18 is a required one-time manual step for those testers.
10. **Invalid metadata is refused.** Unsigned, tampered, downgraded, wrong-product, wrong-channel or checksum-mismatched metadata is rejected. This is intentional and means an invalid feed cannot make an update actionable.
11. **No general downgrade support.** The update client refuses older versions. Running an older installer manually is possible, but data written by a newer build may not be understood by the older one. Back up local data before rolling back.

## Reporting and privacy

12. **Reports are email drafts, not automatic delivery.** Settings > Help & feedback prepares a complete message to `madebytanishk@gmail.com` in your own mail app. You review it and press Send. Juno has no reporting backend and cannot confirm delivery.
13. **No verified inbox receipt.** Release qualification did not include a configured mail client, so receipt in the owner's inbox has not been independently confirmed.
14. **No unattended crash upload.** Crash records stay on this PC under `%APPDATA%\Juno`. The next launch offers a reviewed email draft. Nothing is sent automatically.
15. **Optional diagnostics only.** Diagnostics are off until you choose them. They contain allowlisted technical fields, never prompts, files, screenshots or credentials.
16. **Long reports are shortened in the email draft.** If the report exceeds the mail-link budget, the draft states how many characters fit. Use Copy Report or Save Report to keep the complete document.

## Capability qualification

17. **Real-provider workflows were not re-qualified in the final release pass.** Earlier live acceptance evidence exists for the main routes, but the final rc.18 campaign focused on reporting, updates, animation and release integrity. Provider behavior, models and limits can change independently of Juno.
18. **Command Code is the best-qualified provider route.** Other providers may be visible but are less tested. Use the provider you actually have an account for.
19. **Composio live external connections are not qualified.** The integration surface exists, but no authorized live Composio connection was exercised for this Beta.
20. **Phone and Tailscale connectivity are deferred.** Remote phone pairing, Tailscale Serve/Funnel paths and mobile companion flows are not part of Beta 0.3.
21. **No enforceable workspace-wide spending hard cap.** Per-run paid-route authorization exists in Code Orchestrate, but there is no global hard limit that can guarantee a spend ceiling across every route.
22. **Voice dictation has limited evidence.** Local Windows speech output is available. Human dictation was qualified on one machine only; accuracy, noisy rooms and long sessions are not guaranteed.
23. **Research can return partial results.** The evidence pipeline reads real sources and records citations. When the source-read budget is exhausted, the report says so; narrative synthesis is opt-in and not guaranteed.
24. **Computer and browser tools depend on the packaged driver and permissions.** They are only active when the relevant capability is enabled and the runtime is available. They were not re-qualified in the final pass.
25. **PowerPoint and FFmpeg are optional external tools.** PowerPoint is needed for slide-image previews and PDF export from PPTX. FFmpeg is needed for procedural video. Without them, Juno should show an honest unavailable state rather than pretend output exists.
26. **The frozen 30-task benchmark was not run.** No pass rate is claimed.
27. **Some inherited surfaces are visible but not qualified for Beta 0.3.** Teams, organization, Cloud, mobile pairing, backups and routines exist in the codebase from earlier work. Do not treat every visible control as a tested Beta capability.

## Reporting a problem

Use **Settings > Help & feedback > Report a bug**, then **Open Email Draft**. Include the Juno version, Windows version, feature, expected and actual behavior, steps to reproduce and whether it repeats. Remove API keys, tokens, cookies, private file paths and personal documents before sending.

See [FEEDBACK.md](FEEDBACK.md) for the full guidance and [INSTALL.md](INSTALL.md) for installation troubleshooting.
