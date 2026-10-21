# Juno Beta 0.1 — Release Notes

**Version:** `1.0.0-rc.7` · **Product label:** Juno Beta 0.1 · **Date:** 2026-10-22
**Platform:** Windows 11 x64 · **Installer:** `juno-1.0.0-rc.7-setup.exe`

## What this Beta is

A private, Windows-only desktop workspace for a personal AI agent and coding work. It is not a
general availability release and does not carry the frozen 30-task benchmark.

## What was stabilized in this candidate

- The installed Windows application launches, onboards, connects a provider and runs live Agent and
  Code turns.
- Code model selection is exact: the tested route is
  `commandcode/deepseek/deepseek-v4.1-flash`; run records and the engine session show the same model
  and no fallback.
- Tool permissions work: a denied command did not execute; an `Allow once` approval executed the
  same command and returned its real output.
- Artifacts work end-to-end: real editable PPTX, PowerPoint slide preview, PDF export, and a real
  procedural MP4 with distinct scenes.
- Packaged native helpers resolve correctly, so PowerPoint preview/PDF and Windows local speech
  output work from the installed app.
- The installer has consistent Juno icons, metadata, Start-menu/desktop shortcuts, a working
  uninstaller and a clean reinstall.
- Forced-kill recovery and corrupt-run-record quarantine were exercised on the installed app.
- Results and task status now distinguish a created artifact from an optional visual-QA failure.
  A deck is not reported as a failed task just because PowerPoint is absent.
- The Code model picker has search and provider grouping.
- About/Help/Feedback point at this private Beta repository.
- The inert update feed no longer logs DNS failures on every launch.

## Verify

```text
2209AD0A24D51743CB92FDD7AE34BF9BB60F2F648BE5F9E8BE564180B502D3EE  juno-1.0.0-rc.7-setup.exe
```

The installer is **unsigned**. SmartScreen may warn. See [`INSTALL.md`](INSTALL.md) and
[`KNOWN_ISSUES.md`](KNOWN_ISSUES.md).

## Disclosed limitations

- No independent clean-Windows installation evidence; host acceptance only.
- Human microphone dictation and voice barge-in not qualified.
- Orchestrate Beta live review/repair not re-qualified; parallel mutating Code work disabled.
- Automatic repair disabled.
- Research is a deterministic evidence pipeline; narrative synthesis is opt-in and was not
  authorized.
- PowerPoint and FFmpeg are optional external dependencies.
- Auto-update is not configured.
- The 30-task benchmark was not executed.

Do not use this Beta for irreversible production work without a backup.
