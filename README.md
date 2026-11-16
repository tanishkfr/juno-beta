# Juno v0.5.1 Beta — Security & Reliability

Juno is a Windows desktop workspace for a personal AI agent and coding work.
This repository is the public download and feedback channel for **Juno v0.5.1 Beta**.

**[Download Juno v0.5.1 Beta](https://github.com/tanishkfr/juno-beta/releases/tag/v0.5.1-rc.1)**

Windows 11 x64 · Public Beta · Unsigned installer · Manual updates

> The public release is titled **v0.5.1**. The installed application reports
> **`0.5.1-rc.1`**. The signed update feed still describes the previous beta (`0.4.2-rc.3`);
> v0.5.1 is a manual download. This is not a stable general-availability release.

## What changed in v0.5.1

**A security and reliability maintenance release.**

### Security

- **Separate Windows accounts are isolated.** v0.5.0 could expose some local Juno data to
  another Windows user on the same PC under specific local conditions. v0.5.1 requires the
  desktop capability, or a paired session, for local data routes. Health and static identity
  routes remain public.
- **Existing v0.5.0 users should upgrade manually.** The old build remains exposed until it is
  replaced.
- **Port conflicts fall back cleanly** instead of failing with an address-in-use error.

### Reliability

- OpenCode's managed 2.x runtime installs and discovers models without an app restart.
- Provider cards and model selections remain available across restarts.
- ChatGPT single-model save, restart state and quota-error classification are fixed.
- A reasoning-only response is no longer presented as a final answer.
- A stale local conversation pointer recovers to the companion's valid conversation without
  deleting stored messages.
- Conversation and model state persist after restart.

### Usability

- Clearer provider requirement, setup and status messages.
- Companion selection uses radio/arrow-key semantics.
- Settings navigation, provider rows and selected states are clearer.
- The right-side workspace panel slides in Bot and Code modes and sits closer to the
  conversation; the Code panel's top tab spacing is corrected.

## Download and verify

There is **one installer** for this release.

| File | Size | SHA-256 |
|---|---:|---|
| `juno-0.5.1-rc.1-setup.exe` | 261,849,280 B | `A4375A29888956BE688ADB1BC714A10D2F84B04BCB349676ABCA9B0CED3B09BF` |

Also download `SHA256SUMS.txt` from the same release. In PowerShell:

```powershell
Get-FileHash .\juno-0.5.1-rc.1-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

The installer is **unsigned**. Windows may show Unknown Publisher or SmartScreen. Continue only
if the checksum matches. Do not disable Windows security protections.

## Requirements

- **Windows 11 x64** — the only qualified platform for this beta.
- **A provider account** for external models; account, network and quota are your responsibility.
- **Code work additionally needs the external OMP runtime.** Boreal, Ariadne and Codex are
  bundled; OMP is not.
- **No administrator rights** — installation is per user.
- **Manual updates** — Juno does not download or install updates automatically.

## Upgrade from v0.5.0

Keep a backup if you want a rollback path, close Juno, verify the checksum, run the installer,
then reopen Juno. Companions, conversations, provider settings, model selections, Mission/Code
history and preferences are preserved by the in-place upgrade. There is no in-place downgrade;
restore a backup into a fresh profile if needed.

## Known issues and support

- [Known issues](KNOWN_ISSUES.md)
- [Installation and upgrade](INSTALL.md)
- [Privacy](PRIVACY.md)
- [Feedback](FEEDBACK.md)
- [Versioned v0.5.1 registry](support/v0.5.1-rc.1/known-issues.json)
- [All releases](https://github.com/tanishkfr/juno-beta/releases)

Provider quota is external. The test account used for this beta was over its ChatGPT
Subscription Sharing quota, so a real ChatGPT-plan response is not claimed as qualification.
