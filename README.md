# Juno v0.4.2 Beta — Performance & Polish

Juno is a Windows desktop workspace for a personal AI agent and coding work.
This repository is the public download and feedback channel for
**Juno v0.4.2 Beta**.

**[Download Juno v0.4.2 Beta](https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.2)**

Windows 11 x64 · Public Beta · Unsigned installer · Manual updates

> **Version note:** the public beta is titled **v0.4.2**. The installed
> application reports its internal build version as **`0.4.2-rc.3`**. The
> signed update feed uses `0.4.2-rc.3` so the published build recognizes itself
> as up to date. This is not a stable `0.4.2` binary.

## What is in Juno

- **Bot Mode** — conversations with the providers you connect, streaming
  replies, tools, approvals, memory, routines and a result library.
- **Code Mode** — a workspace agent (Boreal/OMP) that can inspect a project,
  propose edits, ask for permission, run checks and apply changes.
- **Council** — an optional planner and independent reviewer around Bot and Code
  work. Off by default.
- **`/btw`** — a side conversation with its own task, budget and transcript, so
  a question does not disturb the main task.
- **Windows integration** — optional browser automation, computer control,
  local speech (System.Speech fallback plus optional Whisper) and notifications.
- **Local-first storage** — conversations, bots, memory, routines and work
  items stay on this PC. Traffic goes only to the providers and tools you
  connect.

## What changed in v0.4.2

**Performance and polish, with the existing product boundaries preserved.**

- **Fewer reported input tokens.** In the matched Phase 1 short-turn benchmark,
  Juno reported approximately **80.5% fewer input tokens** through task-aware
  tool exposure and a smaller direct-turn catalogue. This is a measured
  benchmark result, not a promise that every task or provider uses 80.5% fewer
  tokens.
- **Smaller compact installer.** The compact installer is **252.3 MB**, down
  from **271.7 MB** in v0.4.1.
- **Faster startup and readiness on the tested Windows host.** The renderer
  now reports shell, first transcript and composer-ready marks. Warm health and
  page readiness improved in the qualification run; absolute times remain
  host- and provider-dependent.
- **Modular optional Android and cloudflared runtimes.** Android platform tools
  and cloudflared are optional downloads with version, size and SHA-256
  verification. They can be installed, verified, repaired and removed from
  Settings. Codex, Boreal/OMP and CUA remain bundled and are not optional.
- **Capability selection during onboarding.** Chat, Coding, Browser, Computer
  control, Android devices, Local voice and Remote access are presented with
  their purpose, size and offline behaviour. Existing profiles skip the
  journey.
- **Runtime management and storage cleanup in Settings.** A single
  Runtimes & storage surface shows readiness, provider health, measured storage
  and safe removal. Removal fails closed while work or a session still owns a
  runtime.
- **Improved Code Mode result validation.** Explicit content requirements are
  checked against the staged workspace, not only against file existence. A
  verified change remains staged until you apply it; applying records
  completion, and discarding, rollback or failed validation is reported
  honestly.
- **More reliable browser session cleanup.** The model can close its own tab or
  browser session with session-scoped tools; it cannot close your browser or
  another application's browser. Cancellation and app exit release owned
  sessions.
- **Installer identity safeguards.** Named production/test profiles are checked
  before and after packaging and before installation. A test installer cannot
  claim the production identity.
- **Codex subscription support preserved.** The ChatGPT-plan Codex route and
  the exact model pins remain unchanged.

Boreal, Pi and OMP remain bounded execution components. This release does not
remove them, and it does not replace your providers.

## Performance

Qualified measurements from the final candidate on the same Windows 11 x64
machine:

| Measurement | Result |
|---|---:|
| Warm health median | 3,253 ms |
| Warm first renderer body median | 6,479 ms |
| Composer-ready median | 6,372 ms |
| Compact installer | 252.3 MB (252,282,304 B) |
| Full/offline installer | 488.6 MB (488,599,330 B) |

These are measurements, not guarantees. Provider latency, network conditions
and the selected model dominate reply time.

## Choose your download

| Variant | File | Size | Installed | Use when |
|---|---|---:|---:|---|
| **Compact (recommended)** | `juno-0.4.2-setup.exe` | 252,282,304 B | about 1.05 GB | You have internet access and can install the browser/Whisper assets when needed. |
| **Full/offline** | `juno-0.4.2-full-setup.exe` | 488,599,330 B | about 1.50 GB | You want the browser engine, Whisper model, Android tools and cloudflared present on first launch. |

The full variant includes offline-capable **runtime assets**. It is not an
entirely offline AI assistant: external model providers still need an account,
network access and available quota.

## Verify before installing

Download the installer and `SHA256SUMS.txt` from the same release. In
PowerShell:

```powershell
Get-FileHash .\juno-0.4.2-setup.exe -Algorithm SHA256
Get-FileHash .\juno-0.4.2-full-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected:

```text
4ab457a97c0fb768768720adcc7c9af4bc5899fef5d2d070d15176c51aa5522b  juno-0.4.2-setup.exe
8f73fe74e983ac217bfc15f4c71b34b3a72dac2072617a2ac497a328c126f278  juno-0.4.2-full-setup.exe
```

If a hash differs, do not install. Delete the file and download it again.

The installer is **unsigned**. Windows may show Unknown Publisher or
SmartScreen. Continue only if the checksum matches. Do not disable Windows
security controls. Some managed PCs may block the installer; stop and ask your
administrator if that happens.

## Documentation

- [Install and upgrade](INSTALL.md)
- [Known issues and limitations](KNOWN_ISSUES.md)
- [Security and integrity](SECURITY.md)
- [Feedback](FEEDBACK.md)

Nothing in this repository is a substitute for the checksum: the release page
and the checksum are hosted by the same publisher. SHA-256 proves integrity,
not publisher identity.
