# Juno v0.4.1 Beta — Unified Agent Runtime

Juno is a Windows desktop workspace for a personal AI agent and coding work.
This repository is the public download and feedback channel for the
**Juno v0.4.1 Beta**.

**[Download Juno v0.4.1 Beta](https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.1)**

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

## What changed in v0.4.1

**One shared task system now runs across Juno's execution experiences.** Bot
Mode, Code Mode, Council, `/btw`, room/team conversations and delegated work
record task identity, lifecycle, cancellation, recovery, model-call accounting
and permission state through the same Juno runtime. This is an internal
consistency change: it does not replace your providers or make the underlying
models faster or smarter.

Specific improvements:

- **Shared task identity and lifecycle across Bot Mode and Code Mode.** A task
  keeps one durable identity from admission to its terminal record.
- **Council planner/reviewer call tracking.** Planner and reviewer calls are
  durable task calls with their own model, usage and terminal state. The parent
  task waits for the mandatory reviewer before it settles.
- **`/btw` side-task identity and isolation.** The side task has its own
  profile, parent relationship, transcript, budget and cancellation, while the
  main task keeps running independently.
- **Room/team conversations in the same task system.** A room turn creates one
  room profile task; each participating member call is recorded under it with
  actor, model and usage.
- **More reliable cancellation and interrupted-task handling.** Cancellation
  settles the task through the runtime instead of leaving a partial record. A
  late provider completion cannot reopen a finished task.
- **Durable usage and terminal records.** A task settles once, with one terminal
  receipt. Duplicate completion events cannot double-charge a task. Usage that
  arrives after settlement is recorded separately as late usage.
- **Stronger Code Mode model-selection boundaries.** An exact Code model is
  checked against the live worker catalogue before work starts, and Juno
  verifies the model Boreal actually bound. A silent substitution or unreviewed
  fallback stops the run.
- **Continued Ariadne verification.** Ariadne remains independent: no executor
  may mark its own claims verified, and Code review or Council verdicts remain
  advisory evidence.
- **Crash-notice behavior qualified.** A hard process kill does not fabricate a
  notice or a reply. A recorded renderer error offers the reviewed crash-report
  action once, and dismissal is durable.
- **Existing app performance preserved.** The Juno-controlled durable task
  overhead is unchanged at roughly 7 ms p50 in the qualification microbenchmark.
- **Existing compact/full distribution options.** The compact installer remains
  the default; the full/offline variant bundles the optional browser engine and
  Whisper model.

Boreal, Pi and OMP remain bounded execution components behind the Juno task
system. Boreal still coordinates Code execution, OMP remains the Code worker
runtime, and Pi remains a provider/agent executor. This release does not remove
them.

## Performance

Qualified measurements from the final candidate on the same Windows 11 x64
machine and tested provider route:

| Measurement | Result |
|---|---:|
| Warm short reply, end to end | **2.29–2.92 s** |
| Durable task overhead | **7.06 ms p50** |
| Compact installer | **271.7 MB** (271,664,867 B) |
| Full/offline installer | **488.6 MB** (488,550,122 B) |

These are measurements, not guaranteed timings. Provider latency, network
conditions and the selected model dominate reply time. The runtime change did
not make the underlying models faster or smarter.

## Choose your download

| Variant | File | Size | Installed | Use when |
|---|---|---:|---:|---|
| **Compact (recommended)** | `juno-0.4.1-setup.exe` | 271,664,867 B | about 1.05 GB | You have internet access and can install the browser/Whisper assets when needed. |
| **Full/offline** | `juno-0.4.1-full-setup.exe` | 488,550,122 B | about 1.50 GB | You want the browser engine and Whisper model present on first launch. |

The full variant includes offline-capable **runtime assets**. It is not an
entirely offline AI assistant: external model providers still need an account,
network access and available quota.

## Verify before installing

Download the installer and `SHA256SUMS.txt` from the same release. In
PowerShell:

```powershell
Get-FileHash .\juno-0.4.1-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected:

```text
3B6B3EF3EC870CA779E1A7B623A3D970D468729F0B9BF2608B171F2400233EBD  juno-0.4.1-setup.exe
C64A3441209BECB10A569498C8FDF403C41592EE5779880B98B8576BAA8CD864  juno-0.4.1-full-setup.exe
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

## Upgrading from v0.4.0

Installing v0.4.1 over v0.4.0 is an in-place upgrade. It uses the same
application identity (`com.agent.app`, product `Juno`, install directory
`%LOCALAPPDATA%\Programs\juno`), so bots, conversations, work items, memory,
provider configuration and credentials stay in place.

- Back up `%USERPROFILE%\.juno` and `%APPDATA%\Juno` first, and keep the v0.4.0
  installer for rollback.
- v0.4.0 remains available at
  <https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.0>.
- A v0.4.0 rollback opens the newer work-item database through its documented
  newer-schema tolerance and rewrites the schema-version metadata. The data
  remains readable, and reinstalling v0.4.1 restores the newer schema. Back up
  before rolling back.

## Known limitations

- **Unsigned Windows executable.** No Authenticode publisher identity and no
  SmartScreen reputation. Windows may warn or, on managed systems, block
  installation.
- **Manual updates.** Juno does not download or run installers. The signed
  automatic-installer upgrade path is not qualified. The authenticated
  announcement feed only reports that a newer release exists and opens the
  release page.
- **Provider accounts, subscriptions, quotas and network access are required**
  for external models. Bundled runtime assets do not remove that requirement.
- **Spending controls are bounded.** A workspace-wide hard spending cap remains
  unenforceable across some external provider routes, and Boreal internal worker
  iterations are not all bounded by Juno's model-call ceiling.
- **Speech acceptance is partial.** Installed speech components and local
  Whisper transcription passed, but live microphone recording was not exercised
  during final qualification.
- **Browser close is model-dependent.** The tested model omitted a required
  `tabId` on its initial browser-close call. Juno reported the error and the
  session was subsequently released.
- **Optional downloads in the compact build.** Browser automation needs the
  pinned agent-browser plus Chrome for Testing. Local Whisper needs the 148 MB
  base.en model. System.Speech works without the Whisper model.
- **Qualification was not a clean-room VM.** The real installed full/offline
  variant was tested on the owner's existing Windows environment. Computer
  control used a packaged read-only runtime probe rather than a full
  model-driven interaction.

See [KNOWN_ISSUES.md](KNOWN_ISSUES.md) for the complete list.

## Security and updates

- The installers are **NotSigned**. SHA-256 is the integrity check; it is not a
  publisher identity check.
- Obtain installers only from this repository's releases. Do not use mirrors.
- Installation and updates are **manual**. Juno may check Ed25519-signed
  release metadata and show release notes, but it never downloads or executes
  an installer.
- The packaged `app-update.yml` points at the reserved host
  `updates.invalid`; the signed feed is announcement-only.
- See [SECURITY.md](SECURITY.md) for the full security note.

## Previous release

Juno v0.4.0 Beta — Intelligence & Efficiency remains available, with its
original installers and checksums:

<https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.0>

Historical notes: [RELEASE_NOTES_v0.4.0.md](RELEASE_NOTES_v0.4.0.md).

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

**Juno v0.4.1 Beta — Unified Agent Runtime**  
Released: 2026-11-10  
Windows x64 · Public Beta · Unsigned · Manual updates
