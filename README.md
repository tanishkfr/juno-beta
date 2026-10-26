# Juno Beta 0.3 (Final)

Juno is a Windows desktop workspace for a personal AI agent and coding work. This repository is the private download and feedback channel for **Juno Beta 0.3 (Final)**, version `1.0.0-rc.18`.

**[Download the current build](https://github.com/tanishkfr/juno-beta/releases/tag/v1.0.0-rc.18)**

Windows 11 x64 · Private beta · Unsigned installer

## What is in Juno

- **Agent conversations** with six built-in city companions, tool calls, inline approvals, memory, routines and a result library.
- **Code workspace** with project attachment, Code, Ask and Orchestrate modes, model selection, staged review, apply/discard, a terminal and preview surfaces.
- **Teams and shared work** surfaces for conversation handoff and collaboration.
- **Research** with recorded sources and citations, plus browser and computer tools when you authorize them.
- **Local Windows speech output**, with no cloud speech service required.
- **Local-first storage** for conversations, agents, memory, routines and artifacts. External traffic goes to the providers and tools you connect.

The Beta is deliberately narrow. Read [KNOWN_ISSUES.md](KNOWN_ISSUES.md) before installing.

## Requirements

- **Windows 11 x64.** Windows 10, macOS and Linux are not qualified for this Beta.
- **A GitHub invitation.** This repository is private. Ask the owner to invite your GitHub account as a read collaborator. A copied release link does not grant access.
- **A supported provider account.** Command Code is the best-qualified route in this Beta. Other provider rows may be available but are less tested. You need your own account and API access.
- **About 1 GB free disk space** for the application and generated work.
- **Optional:** Microsoft PowerPoint for slide-image previews and PDF export from generated presentations; FFmpeg on `PATH` for procedural video generation.

## Download, verify and install

1. Open the [Juno Beta 0.3 (Final) release](https://github.com/tanishkfr/juno-beta/releases/tag/v1.0.0-rc.18).
2. Download `juno-1.0.0-rc.18-setup.exe` and `SHA256SUMS.txt`.
3. Verify the installer before running it:

   ```powershell
   Get-FileHash .\juno-1.0.0-rc.18-setup.exe -Algorithm SHA256
   ```

   Expected SHA-256:

   ```text
   D28E79636D19BAABC7CC9DA8D926519211AFF4F3BE0335641865A768404AC2A0
   ```

   Expected file size: `391,808,044` bytes.

   If the hash differs, do not install. Delete the file and download it again.

4. The installer is **unsigned**. Windows may show Unknown Publisher or SmartScreen. Only continue if the checksum matches, and do not disable Windows security controls.
5. Follow [INSTALL.md](INSTALL.md) for the full installation, upgrade, troubleshooting and uninstallation steps.

The rc.18 installer is a one-click, per-user installation. It installs in place over an earlier Juno Beta installation; it does not install side by side. The rc.18 NSIS installer has not been executed in a fresh independent Windows environment, so a real installed-app journey is still pending independent confirmation. See [INSTALL.md](INSTALL.md) and [KNOWN_ISSUES.md](KNOWN_ISSUES.md).

## First run

- Complete the short setup: name, starting companion and optional provider connection.
- The product tour introduces the real workspace and can be replayed from **Settings > Help & feedback**.
- Try a small Agent question, or open **Code** and choose a disposable project folder.
- Generated results appear in the **Library**. Presentations are editable PPTX files; previews and PDF export use PowerPoint when it is installed.

## Updates

Juno checks a signed update feed after launch and every six hours. **Settings > Updates** shows the current version, any available release and the owner's notes.

- Update metadata is authenticated with Ed25519. Unsigned, tampered, downgraded or wrong-channel metadata is refused.
- The installer is unsigned, so installation is always manual. Juno never downloads or runs the installer for you.
- **Open Beta releases** takes you to this release page. **Verify downloaded installer** checks a downloaded file against its checksum file.
- Builds before rc.18 cannot discover updates. Installing rc.18 is a one-time manual step for those testers.

## Feedback

The primary route is inside Juno: **Settings > Help & feedback > Report a bug**, then **Open Email Draft**. Juno prepares a complete email to `madebytanishk@gmail.com` in your own mail app. You review it and press Send yourself; Juno does not send it and cannot confirm delivery.

You can also open an issue in this repository if you have access. See [FEEDBACK.md](FEEDBACK.md) for what makes a useful report, how long reports are handled and how to redact private information.

## Known limitations

- The installer is unsigned and updates are manual.
- The rc.18 NSIS install and uninstall journey is not yet independently verified.
- Live external Composio connections are not qualified for this Beta.
- Phone and Tailscale connectivity are deferred.
- No enforceable workspace-wide spending hard cap is available.
- Real-provider workflows were not re-qualified in the final release pass; earlier live evidence exists, but provider behavior can change.
- The full list is in [KNOWN_ISSUES.md](KNOWN_ISSUES.md).

## Privacy and licensing

Read [PRIVACY.md](PRIVACY.md) for what stays on your computer, what is sent to providers or tools, how diagnostics and crash records work, and what the update check sends.

Juno is Apache-2.0 licensed. The repository includes the product license, upstream NOTICE and third-party notices. See [LICENSES.md](LICENSES.md) and [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

## Access policy

This repository is private and the installer is for invited testers only. Do not redistribute the installer, the repository contents or your access. Access can be removed at any time.
