# Juno v0.4.0 Beta — Intelligence & Efficiency

Juno is a Windows desktop workspace for a personal AI agent and coding work.
This repository is the public download and feedback channel for the
**Juno v0.4.0 Beta**.

**[Download Juno v0.4.0 Beta](https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.0)**

Windows 11 x64 · Public Beta · Unsigned installer · Manual updates

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

## What changed since Beta 0.3

- **Intelligence & Efficiency.** Council and `/btw` add deliberate planning,
  independent review and side conversations without changing the ordinary chat
  path.
- **Faster everyday replies on the qualified route.** The earlier
  CommandCode/DeepSeek qualification measured about 39–44 ms of Juno dispatch
  and 2.4–3.0 seconds for a short warm reply. The final packaged Codex smoke
  measured about 5–7 seconds end to end. Provider latency dominates; these are
  measurements, not guarantees.
- **Smaller compact installer.** About 272 MB, down from about 504 MB for the
  previous candidate. Installed compact footprint is about 1.05 GB.
- **Reliability and recovery.** Stale data-directory lease recovery on Windows
  11 without `wmic`, a bounded renderer reload after a crash, and clearer
  provider errors.
- **Optional runtime downloads.** The compact build omits the browser engine and
  local Whisper weights; both are pinned, user-requested downloads. The
  full/offline variant includes them.

## Choose your download

| Variant | File | Size | Installed | Use when |
|---|---|---:|---:|---|
| **Compact (recommended)** | `juno-0.4.0-setup.exe` | 271,652,163 B | about 1.05 GB | You have internet access and can install the browser/Whisper assets when needed. |
| **Full/offline** | `juno-0.4.0-full-setup.exe` | 488,536,955 B | about 1.50 GB | You want the browser engine and Whisper model present on first launch. |

The full variant includes offline-capable **runtime assets**. It is not an
entirely offline AI assistant: external model providers still need an account,
network access and available quota.

## Verify before installing

Download the installer and `SHA256SUMS.txt` from the same release. In
PowerShell:

```powershell
Get-FileHash .\juno-0.4.0-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected:

```text
4AF07ECD32F8769524A7A72E027930E85CF793B46C23E1AB49C7305877BE2942  juno-0.4.0-setup.exe
554CA46E69903E44DBAD1AECB273737522B6C89CD6DA0412FC0985F19319BBE8  juno-0.4.0-full-setup.exe
```

If the hash differs, do not install. Delete the file and download it again.

The installer is **unsigned**. Windows may show **Unknown Publisher** or a
SmartScreen warning. Continue only if the checksum matches. Do **not** disable
Microsoft Defender, SmartScreen, Smart App Control or any other security
control. Some managed PCs may block unsigned installers; in that case stop and
ask your administrator.

## Install

1. Close any running Juno window.
2. Run the installer. It is a per-user installation and does not require
   administrator rights.
3. It installs in `%LOCALAPPDATA%\Programs\juno`, creates a **Juno** Start menu
   entry and desktop shortcut, and registers **Juno** in
   **Settings > Apps > Installed apps**.
4. Open Juno and complete setup. No Juno account is required.

See [INSTALL.md](INSTALL.md) for the full guide, including upgrade, rollback,
optional runtime downloads and troubleshooting.

## Upgrading from Beta 0.3

A direct manual upgrade from `1.0.0-rc.18` (Beta 0.3 Final) to `0.4.0` was
tested with data preservation. The installer uses the same application identity
(`com.agent.app`, product `Juno`, install directory
`%LOCALAPPDATA%\Programs\juno`), so it upgrades in place.

- Back up `%USERPROFILE%\.juno` and `%APPDATA%\Juno` first, and keep the
  previous installer for rollback.
- You do **not** need to install `1.0.0-rc.21` first for the manual path. The
  signed automatic-update bridge is a separate, unqualified path and is not used
  here.
- The in-app installer verifier accepts `juno-0.4.0-setup.exe` as the approved
  manual migration from the `1.0.0-rc` Beta 0.3 line.

## Known limitations

- **Unsigned Windows executable.** No Authenticode certificate and no
  SmartScreen publisher reputation. Windows may warn or, on managed systems,
  block installation.
- **Manual updates.** Juno does not download or run installers. The signed
  automatic-update bridge from the old `1.0.0-rc` line is not qualified and must
  not be represented as working.
- **Provider accounts, subscriptions, quotas and network access are required**
  for external models. Bundled runtime assets do not remove that requirement.
- **Optional downloads in the compact build.** Browser automation needs the
  pinned agent-browser plus Chrome for Testing (about 160 MB download, about
  450 MB on disk). Local Whisper needs the 148 MB base.en model. System.Speech
  works without the Whisper model.
- **Screen-reader acceptance is partial.** Keyboard navigation, visible focus,
  contrast, zoom, forced colours and reduced motion were checked. A real
  NVDA/Narrator speech-output session was not completed.
- **Council and model-driven browser/computer coverage are bounded.**
- **No enforceable workspace-wide spending hard cap.**

See [KNOWN_ISSUES.md](KNOWN_ISSUES.md) for the complete list.

## Security and updates

- The installers are **NotSigned**. SHA-256 is the integrity check; it is not a
  publisher identity check.
- Obtain installers only from this repository's releases. Do not use mirrors.
- Installation and updates are **manual**. Juno may check Ed25519-signed
  release metadata and show release notes, but it never downloads or executes
  an installer.
- See [SECURITY.md](SECURITY.md) for the full security note.

## Feedback

Use **Settings > Help & feedback > Report a bug** to prepare a reviewed email
draft, or open an issue at
<https://github.com/tanishkfr/juno-beta/issues>. Remove API keys, tokens,
cookies and private file paths before sending.

## Licensing

Juno is licensed under the Apache License 2.0. It is a derivative work of the
open-source OpenMausBot project; the required attribution and third-party
notices are preserved in [LICENSING.md](LICENSING.md),
[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md) and the packaged
`licenses/` folder. The upstream name and mascot are trademarks of their owner;
this project does not claim them.

---

**Juno v0.4.0 Beta — Intelligence & Efficiency**  
Released: 2026-11-10  
Windows x64 · Public Beta · Unsigned · Manual updates
