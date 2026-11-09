# Juno v0.4.0 Beta — Intelligence & Efficiency

**Public Beta · Windows x64 · Version 0.4.0 · Unsigned installer · Manual updates**

Juno is a local-first Windows desktop workspace for a personal AI agent and
coding work. This release adds Council and `/btw`, keeps Bot and Code Mode,
and makes the compact installer substantially smaller.

## Download

| Variant | File | Size |
|---|---|---:|
| **Compact (recommended)** | `juno-0.4.0-setup.exe` | 271,652,163 B |
| **Full/offline** | `juno-0.4.0-full-setup.exe` | 488,536,955 B |

The full variant includes the pinned browser engine and Whisper base.en model.
External model providers still need internet access, an account and quota.

## Verify before installing

```powershell
Get-FileHash .\juno-0.4.0-setup.exe -Algorithm SHA256
Get-FileHash .\juno-0.4.0-full-setup.exe -Algorithm SHA256
```

Expected:

```text
4AF07ECD32F8769524A7A72E027930E85CF793B46C23E1AB49C7305877BE2942  juno-0.4.0-setup.exe
554CA46E69903E44DBAD1AECB273737522B6C89CD6DA0412FC0985F19319BBE8  juno-0.4.0-full-setup.exe
```

The installer is **unsigned**. Windows may show Unknown Publisher or
SmartScreen. Continue only if the checksum matches. Do not disable Windows
security controls. Some managed PCs may block the installer; stop and ask your
administrator if that happens.

## What changed since Beta 0.3

- **Council** — an optional planner and independent reviewer around Bot and Code
  work. Off by default; every role is validated against the live model
  catalogue.
- **`/btw`** — a side conversation with its own task, budget and transcript.
  The main task keeps running; cancellation is independent.
- **Faster everyday replies on the qualified route.** The earlier
  CommandCode/DeepSeek qualification measured 39–44 ms of Juno dispatch and
  about 2.4–3.0 seconds for a short warm reply. The final packaged Codex smoke
  measured about 5–7 seconds end to end. Provider latency dominates; these are
  measurements, not guarantees.
- **Cold first-turn dispatch** improved from 2.699 s to 1.724 s in a matched A/B
  on the earlier route.
- **Smaller compact installer** — about 272 MB, down from about 504 MB, with a
  compact installed footprint of about 1.05 GB.
- **Code Mode** keeps its bundled Boreal coordinator, real file edits,
  permission cards and bounded recovery.
- **Reliability** — stale data-directory lease recovery on Windows 11 without
  `wmic`; a bounded renderer reload after a crash; honest provider errors.
- **Optional downloads** — the compact build omits the browser engine and local
  Whisper weights; both are pinned, user-requested downloads. System.Speech
  works immediately.

## Upgrade from Beta 0.3

A direct manual upgrade from `1.0.0-rc.18` to `0.4.0` was tested with data
preservation. The installer upgrades in place and keeps bots, conversations,
work items, settings and credentials.

- Back up `%USERPROFILE%\.juno` and `%APPDATA%\Juno` first, and keep the
  previous installer for rollback.
- You do not need to install `1.0.0-rc.21` first for the manual path.
- The signed automatic-update bridge is **not** qualified. Updates are manual.

See [INSTALL.md](https://github.com/tanishkfr/juno-beta/blob/main/INSTALL.md)
for the full upgrade, rollback, optional-download and troubleshooting guide.

## Known limitations

- **Unsigned Windows executable.** No Authenticode publisher identity and no
  SmartScreen reputation. Some managed systems may block installation.
- **Manual updates.** The signed automatic-update bridge from the old
  `1.0.0-rc` line is not qualified.
- **Provider accounts, subscriptions, quotas and network access are required**
  for external models.
- **Optional downloads in the compact build.** Browser automation needs about
  160 MB of downloads and about 450 MB on disk. Local Whisper needs the 148 MB
  base.en model. System.Speech works without it.
- **Screen-reader acceptance is partial.** Keyboard, focus, contrast, zoom,
  forced colours and reduced motion were checked; a real NVDA/Narrator
  speech-output session was not completed.
- **Council and model-driven browser/computer coverage are bounded.**
- **No enforceable workspace-wide spending hard cap.**

See [KNOWN_ISSUES.md](https://github.com/tanishkfr/juno-beta/blob/main/KNOWN_ISSUES.md)
for the complete list. See
[SECURITY.md](https://github.com/tanishkfr/juno-beta/blob/main/SECURITY.md)
for the security note.

## Feedback

Use **Settings > Help & feedback > Report a bug** to prepare a reviewed email
draft, or open an issue at
<https://github.com/tanishkfr/juno-beta/issues>. Remove API keys, tokens,
cookies and private file paths before sending.

---

**Juno v0.4.0 Beta — Intelligence & Efficiency**  
Released: 2026-11-10
