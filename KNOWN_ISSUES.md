# Known Issues — Juno Beta 0.1

Candidate: `1.0.0-rc.7` · Date: 2026-10-22 · Platform: Windows 11 x64

This list is part of the release, not an afterthought. If a feature is listed as unqualified, do
not assume it is production-ready.

## Release-level limitations

1. **Windows only.** macOS and Linux packages are not qualified for this Beta.
2. **Unsigned installer.** SmartScreen may warn. No certificate was available; no signature was
   fabricated.
3. **Limited external-machine evidence.** Installation and acceptance were performed on the
   owner's development PC. External testers are the first independent evidence; clean-VM
   qualification is not complete.
4. **No auto-update channel.** The updater is intentionally dormant. Install a newer candidate
   manually from the private release page.
5. **Frozen 30-task benchmark not run.** 0/30 tasks executed. None of the benchmark results are
   claimed or represented as a pass rate.
6. **Private distribution.** Access requires a GitHub collaborator invitation. A copied release URL
   is not enough.

## Feature limitations

7. **Automatic repair is disabled.** It is not qualified for Beta.
8. **Parallel mutating Code workers are disabled.** Beta serializes mutating work.
9. **Orchestrate · Beta is restricted.** One lead, bounded roster, one writer. A live
   review→repair→re-review completion was not re-established in this campaign; do not rely on it
   for critical work.
10. **Human voice input is not qualified.** Local Windows speech output works, but microphone
    dictation, partial/final transcripts and barge-in were not tested with a human session.
11. **Research is deterministic and may be partial.** It reads real sources, records citations and
    verifies quotes, but narrative synthesis is opt-in and was not authorized. Quick runs may
    exhaust their source budget and return a partial comparison; the report says so.
12. **Computer control is not fully qualified.** The Computer panel and consent copy exist; actual
    screen viewing/control and scaling at 100/125/150% were not exercised.
13. **Teams, organization, Cloud, remote access, mobile pairing, backups and routines** are visible
    inherited surfaces but were not exercised for this Beta. Do not treat them as qualified.
14. **External dependencies:** PowerPoint is needed for slide-image previews and PDF export from
    PPTX; FFmpeg is needed for procedural video. Without them, Juno should show an honest
    warning/blocked state — it must not pretend the output exists.
15. **Installer registry name** shows `Juno 1.0.0-rc.7` while the product UI and release title say
    `Juno Beta 0.1`. This is a cosmetic version-label mismatch.

## Interaction issues found in C.5

16. On a fresh profile with developer CLIs installed but unauthenticated, onboarding provider rows
    may say **"Needs attention"** rather than "Sign in" / "Not connected". It does not block setup;
    use the provider you actually have.
17. A completed read-only Code run can leave the stage chip at
    `Investigating · Read-only` after the answer has finished. The result and status are still
    correct.
18. A sparse `split` presentation can look under-filled; the content is editable and legible.
19. Research source selection is heuristic. A prompt asking for an official source may still read
    secondary pages; always inspect the source list before relying on a claim.

## Reporting

If you hit something not on this list, use the issue templates and include the Juno version,
Windows version, feature, expected/actual behavior, steps, and whether it repeats. Remove API keys,
tokens and personal information from logs or screenshots first.
