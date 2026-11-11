# Installing Juno v0.4.2 Beta

This guide covers the Windows x64 installers for **Juno v0.4.2 Beta —
Performance & Polish**.

## Requirements

- **Windows 11 x64.** Windows 11 is the qualified platform. Windows 10, macOS,
  Linux, ARM64 and 32-bit Windows are not qualified for this Beta.
- **A supported provider account** for external models. Juno does not include
  model capacity, subscriptions or quota.
- **Network access** for provider calls and, in the compact build, for optional
  browser/Whisper downloads.
- **Disk space:** about 1.05 GB for the compact application, or about 1.50 GB
  for the full/offline variant. Leave additional space for projects, generated
  files and backups.
- **No administrator rights required.** The installer is per-user.

## Choose a download

| Variant | File | Size | Notes |
|---|---|---:|---|
| Compact (recommended) | `juno-0.4.2-setup.exe` | 252,282,304 B | Omits the browser engine and Whisper weights; installs them on request. |
| Full/offline | `juno-0.4.2-full-setup.exe` | 488,599,330 B | Includes the pinned browser engine, Whisper base.en model, Android tools and cloudflared. |

Both variants contain the same application code. The full variant adds the
larger optional runtime assets. External providers still need the internet.

## Download and verify

Download the installer and `SHA256SUMS.txt` from the official release:

<https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.2>

In PowerShell, from the download folder:

```powershell
Get-FileHash .\juno-0.4.2-setup.exe -Algorithm SHA256
Get-FileHash .\juno-0.4.2-full-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected SHA-256:

```text
4ab457a97c0fb768768720adcc7c9af4bc5899fef5d2d070d15176c51aa5522b  juno-0.4.2-setup.exe
8f73fe74e983ac217bfc15f4c71b34b3a72dac2072617a2ac497a328c126f278  juno-0.4.2-full-setup.exe
```

The hash is not case-sensitive. If it does not match, stop. Delete the file and
download it again. Do not install a file whose provenance you cannot verify.

On Linux, WSL or Git Bash you can also validate the released checksum file:

```sh
sha256sum --check SHA256SUMS.txt
```

Expected output is `OK` for each installer and exit code `0`.

## Unsigned installer

The installer is **not code-signed**.

- Authenticode status: `NotSigned`.
- There is no verified publisher identity and no SmartScreen reputation.
- Windows may show **Unknown Publisher** or **Windows protected your PC**
  (SmartScreen).
- If SmartScreen appears, choose **More info**, confirm the file name, then
  **Run anyway** — only after the SHA-256 matches.
- Do **not** disable Microsoft Defender, SmartScreen, Smart App Control,
  antivirus software or any other Windows security control.
- Some managed or enterprise PCs block unsigned installers by policy. If
  Windows blocks the installer and you cannot proceed safely, stop and contact
  your administrator. Do not work around a security block.
- The checksum proves integrity, not publisher identity. There is no
  Authenticode signature for this Beta.

## New installation

1. Close any running Juno window.
2. Run the installer. The compact and full installers share the same
   application identity, so installing one over the other is an in-place
   replacement, not a second installation.
3. The installer places the application in
   `%LOCALAPPDATA%\Programs\juno`, creates a **Juno** Start menu entry and a
   desktop shortcut, and registers **Juno** in **Settings > Apps > Installed
   apps**.
4. The installer does not launch Juno automatically.
5. Open Juno from the Start menu or desktop shortcut.

## First run and connecting providers

1. Complete onboarding: display name, starting companion, and any optional
   capabilities you want.
2. Connect at least one provider in Settings. Provider accounts, subscriptions,
   quotas and network access are your responsibility.
3. For the ChatGPT-plan Codex route, sign in with the official Codex flow. Juno
   preserves that subscription route and does not silently redirect it to a
   billable API key.
4. Codex, Boreal/OMP and CUA are bundled. Browser, Whisper, Android tools and
   cloudflared are optional in the compact build and can be installed from
   Settings.
5. Existing profiles skip onboarding. Your bots, conversations, model pins and
   settings are retained.

## Upgrading from v0.4.1

1. Back up your Juno data and keep the v0.4.1 installer available.
2. Close Juno completely.
3. Run the v0.4.2 installer silently or interactively. It upgrades in place and
   preserves bots, conversations, credentials, settings and work items.
4. Open Juno and confirm your provider and model pins.

The v0.4.1 public installer remains available at:

<https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.1>

Use it only after backing up your data. Data written by a newer build may not
be understood by an older build; rollback compatibility is not promised for
future schema versions.

## Full/offline variant

The full installer includes the pinned browser engine, Whisper base.en model,
Android tools and cloudflared. It does not remove the need for internet access
to external model providers. After installation, Settings > Runtimes & storage
should show these bundled assets as ready; nothing needs to be downloaded for
them.

## Uninstall

Use **Settings > Apps > Installed apps > Juno > Uninstall**, or the uninstaller
in `%LOCALAPPDATA%\Programs\juno`. The uninstaller removes the program files.
Your Juno data, conversations and credentials are kept unless you explicitly
reset them.

## Updates

Updates are manual in this Beta. Juno may fetch an Ed25519-signed release
announcement and open the release page. It does not download or run an
installer automatically. See [SECURITY.md](SECURITY.md).
