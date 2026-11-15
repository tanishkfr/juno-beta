# Juno v0.5 Beta — Unified Companion Experience

Juno is a Windows desktop workspace for a personal AI agent and coding work.
Companions, conversations, projects and tasks live in one window, and the data
stays on your PC: conversations, memory, routines and work items are stored
locally, and traffic goes only to the providers and tools you connect.

This repository is the public download and feedback channel for **Juno v0.5
Beta**.

**[Download Juno v0.5 Beta](https://github.com/tanishkfr/juno-beta/releases/tag/v0.5.0-rc.1)** ·
[Install guide](INSTALL.md) ·
[Known issues](KNOWN_ISSUES.md)

Windows 11 x64 · Public Beta · Unsigned installer · Manual updates

> **Version note:** the public beta is titled **v0.5**. The installed
> application reports its internal build version as **`0.5.0-rc.1`**, and
> Settings shows **Juno v0.5 Beta · 0.5.0-rc.1**. This is a release candidate for
> the beta, not a stable `0.5.0` binary. Earlier releases remain available on the
> [releases page](https://github.com/tanishkfr/juno-beta/releases).

## What is in Juno

- **One unified workspace** — a companion-first experience instead of separate
  Bot and Code modes: one sidebar, one composer, one conversation.
- **Companions** — persistent characters with their own instructions, model
  pins, memory and permission scope.
- **Code** — a workspace agent (Boreal/OMP) that inspects a project, proposes
  edits, asks for permission, runs checks and applies changes.
- **Missions** — a previewed, authorized unit of work that hands off to Code and
  keeps its own identity, budget and verification.
- **Ariadne** — local, independent verification of owner-declared checks and
  applied Code revisions.
- **Council** — an optional planner and independent reviewer around Bot and Code
  work. Off by default.
- **Windows integration** — optional browser automation, computer control, local
  speech and notifications.
- **Local-first storage** — conversations, bots, memory, routines and work items
  stay on this PC.

## What changed in v0.5

**The companion-first release, with the v0.4.x engineering boundaries preserved.**

### Unified Juno workspace

The separate Bot/Code mode switch is gone. One workspace carries conversation,
Code and Mission work, and Code stays attached to the conversation that
authorized it.

### Refined companion sidebar

Companion navigation, selected states and pinning were reworked, with Recent Work
organized by project directly below the companion list — no artificial gap, clear
project/task nesting and compact status marks. Profile and Settings remain in the
footer.

### Refined composer

A compact single composer with a clearer input/toolbar hierarchy: attachments and
secondary tools stay in the toolbar, **Code** and **Mission** are first-class
actions, model and permission controls keep their place, and the input expands
cleanly for multiline text.

### Atmospheric empty state

A Juno-inspired pixel sky sits behind a genuinely empty conversation, with the
selected companion's own artwork. It transitions into a neutral reading canvas as
the first message arrives; existing threads open directly in the settled state.
Reduced-motion preferences are respected.

### Light and dark themes

The OLED-black dark skin and the warm light skin were both refined, with contrast
checked across surfaces. Replies and your own messages carry the reading weight;
tool activity and receipts stay quiet.

### Read-only Code

A Code question that asks for an explanation — or that says no file may change —
is a normal, verifiable request. Juno checks the run's own before/after
fingerprints: nothing changed is a pass, and a worker that writes during a
read-only run fails and is never offered for transfer.

### Missions and Ariadne

Missions are previewed with their objective, effects, model route and
authorization boundary before anything runs. A pending decision, the exact child
identity and its attempt survive a restart, without replaying an uncertain side
effect or creating a second child. Ariadne verifies owner-declared checks and
applied revisions.

### Providers and models

ChatGPT-plan catalogues are read from the connected account and report a retry
state instead of a blank list. An explicit model choice is never silently
replaced. A rejected credential found during discovery is reported as an
authentication problem, not a catalogue outage.

### Manual update announcements

A signed manifest can announce a newer release and name its own HTTPS download
page. Nothing is downloaded or installed automatically, and invalid signatures or
unsafe URLs are refused.

## Download

| File | Size |
|---|---:|
| `juno-0.5.0-rc.1-setup.exe` | 261,843,896 bytes (249.7 MiB) |

One installer. There is no separate full/offline variant for this release. The
installer includes the application, the Code coordinator (Boreal), the Ariadne
verifier, the Codex runtime and local speech assets; the browser engine, Android
platform tools and cloudflared are installed on request from Settings.

## Verify before installing

Download the installer and `SHA256SUMS.txt` from the same release, then in
PowerShell:

```powershell
Get-FileHash .\juno-0.5.0-rc.1-setup.exe -Algorithm SHA256
```

Expected:

```text
B8C931EC42D7892B5FA8E64781220A3A270895AD586636801E53C1452CEBB5C6  juno-0.5.0-rc.1-setup.exe
```

The installer is **unsigned**. Windows may show *Unknown publisher* or a
SmartScreen warning. Continue only if the checksum matches, and do not disable
Windows security controls to install Juno. See [SECURITY.md](SECURITY.md).

## Windows requirements

| Requirement | Value |
|---|---|
| Operating system | **Windows 11 x64** (qualified) |
| Architecture | x64 only — ARM64, Windows 10, Linux and macOS are not qualified |
| Network | Required for AI providers and optional downloads |
| Disk | The installer is 249.7 MiB; the installed app and its bundled runtimes need additional space |

## Install or upgrade

1. **Back up first.** In Juno, open **Settings → Backups → Export full backup**,
   or quit Juno and copy `%USERPROFILE%\.juno` to a protected folder.
2. **Quit Juno completely.**
3. **Run `juno-0.5.0-rc.1-setup.exe`** after verifying its SHA-256.
4. **Launch Juno and let it finish starting**; the first start can take longer
   while the workspace opens and supported migrations run.
5. Reconnect any provider whose credentials were not part of your backup.

The full guide, including uninstall and troubleshooting, is in [INSTALL.md](INSTALL.md).
An in-place downgrade is **not supported**; restore a pre-upgrade backup into a
fresh profile instead.

## Provider connections

Juno includes no AI subscription and resells no model access. You connect your
own account and Juno uses it directly (Command Code, Codex/ChatGPT plan, Claude,
Grok, MiniMax, Mistral, OpenAI-compatible endpoints, OpenCode and other ACP
engines). A provider is only usable when your account, plan and this build can
actually use it; availability, catalogues, quotas and billing are controlled by
the provider.

**Code execution additionally requires the external OMP worker runtime.** The
Windows package bundles Juno's Code coordinator, the Ariadne runtime and the
Codex runtime, but it does not bundle OMP.

## Known issues and limitations

The current list is in [KNOWN_ISSUES.md](KNOWN_ISSUES.md), and the same data is
published for the website at [support/v0.5.0-rc.1/known-issues.json](support/v0.5.0-rc.1/known-issues.json).
The most common boundaries:

- **Unsigned installer** — no Authenticode identity, no SmartScreen reputation.
- **Manual updates only** — Juno does not download or install updates for you.
- **No in-place downgrade.**
- **Provider-dependent** — you need your own account, network access and quota.
- **Code needs OMP**, which is not bundled.
- **No workspace-wide spending hard cap.**
- **Ariadne is scoped** to owner-declared checks and Code revisions.
- **Desktop-first** — modeled actions are scoped to the desktop app in this beta.

## Feedback and security

- **Bugs and feature requests:** [open an issue](https://github.com/tanishkfr/juno-beta/issues/new/choose)
  or use **Settings → Help & feedback** in Juno. See [FEEDBACK.md](FEEDBACK.md).
- **Security problems:** do not open a public issue with exploit details. Follow
  [SECURITY.md](SECURITY.md) or email **madebytanishk@gmail.com**.
- **Privacy:** [PRIVACY.md](PRIVACY.md) describes exactly what stays local and
  what leaves your machine.

## Links

- **All releases:** <https://github.com/tanishkfr/juno-beta/releases>
- **This release:** <https://github.com/tanishkfr/juno-beta/releases/tag/v0.5.0-rc.1>
- **Install guide:** <https://github.com/tanishkfr/juno-beta/blob/main/INSTALL.md>
- **Known issues:** <https://github.com/tanishkfr/juno-beta/blob/main/KNOWN_ISSUES.md>
- **Security:** <https://github.com/tanishkfr/juno-beta/blob/main/SECURITY.md>
- **Support and feedback:** <https://github.com/tanishkfr/juno-beta/blob/main/FEEDBACK.md>

---

**Build provenance:** qualified source revision `9a53d13604cbd95d191bb1698fe35f6a019f1936`.
`juno-0.5.0-rc.1-setup.exe`, 261,843,896 bytes, SHA-256
`B8C931EC42D7892B5FA8E64781220A3A270895AD586636801E53C1452CEBB5C6`.
Windows 11 x64 · Unsigned · Manual installation and manual updates.
The application source is private; this repository publishes release
documentation and metadata only.
