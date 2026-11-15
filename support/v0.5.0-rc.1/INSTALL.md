# Installing Juno v0.5 Beta

Version `0.5.0-rc.1` · Windows 11 x64 · Unsigned installer · Manual updates

This guide covers installing, upgrading and uninstalling **Juno v0.5 Beta**. If
something here does not match what you see, check
[KNOWN_ISSUES.md](https://github.com/tanishkfr/juno-beta/blob/main/KNOWN_ISSUES.md) and the
[releases page](https://github.com/tanishkfr/juno-beta/releases).

## Requirements

- **Windows 11 x64.** Windows 11 is the qualified platform. Windows 10, macOS,
  Linux, ARM64 and 32-bit Windows are not qualified for this beta.
- **A supported provider account** for external models. Juno does not include
  model capacity, subscriptions or quota.
- **Network access** for provider calls and for optional runtime downloads.
- **Disk space.** The installer is 249.7 MiB; the installed application and its
  bundled runtimes need additional space. Leave room for projects and backups.
- **No administrator rights required.** The installer is per-user.

## Download

There is **one installer** for this release — no separate full/offline variant.

| File | Size |
|---|---:|
| `juno-0.5.0-rc.1-setup.exe` | 261,843,896 bytes (249.7 MiB) |

Download it and `SHA256SUMS.txt` from the official release:

<https://github.com/tanishkfr/juno-beta/releases/tag/v0.5.0-rc.1>

That release page is the only official source. Do not use third-party mirrors,
repacks or “fixed” installers.

## Verify before running the installer

In PowerShell, from the download folder:

```powershell
Get-FileHash .\juno-0.5.0-rc.1-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected:

```text
B8C931EC42D7892B5FA8E64781220A3A270895AD586636801E53C1452CEBB5C6  juno-0.5.0-rc.1-setup.exe
```

The hash is not case-sensitive. If it does not match, stop: delete the file and
download it again. Do not install a file whose provenance you cannot verify.

On Linux, WSL or Git Bash you can validate the released checksum file:

```sh
sha256sum --check SHA256SUMS.txt
```

Expected output is `OK` and exit code `0`.

## Unsigned installer

The installer is **not code-signed**.

- Authenticode status: `NotSigned`; there is no verified publisher identity and
  no SmartScreen reputation.
- Windows may show **Unknown Publisher** or **Windows protected your PC**
  (SmartScreen).
- If SmartScreen appears, choose **More info**, confirm the file name, then
  **Run anyway** — only after the SHA-256 matches.
- Do **not** disable Microsoft Defender, SmartScreen, Smart App Control,
  antivirus or any other Windows security control.
- Some managed PCs block unsigned installers by policy. If Windows blocks the
  installer and you cannot proceed safely, stop and contact your administrator.
- The checksum proves integrity, not who built the file.

## New installation

1. Close any running Juno window.
2. Run the installer.
3. The installer places the application in `%LOCALAPPDATA%\Programs\juno`, creates
   a **Juno** Start menu entry and a desktop shortcut, and registers **Juno** in
   **Settings → Apps → Installed apps**.
4. The installer does not launch Juno automatically.
5. Open Juno from the Start menu or desktop shortcut.

## First run and connecting providers

1. Complete onboarding: your name, a starting companion, and any optional
   capabilities you want.
2. Connect at least one provider in Settings. Provider accounts, subscriptions,
   quotas and network access are your responsibility.
3. For the ChatGPT-plan Codex route, use the official Codex sign-in. Juno keeps
   that subscription route and does not redirect it to a billable API key.
4. Juno bundles its Code coordinator (Boreal), the Ariadne verifier, the Codex
   runtime and local speech assets. The browser engine, Android platform tools and
   cloudflared are installed on request from Settings.
5. **Code work additionally needs the external OMP runtime**, installed and
   authenticated. Juno does not bundle it.
6. Existing profiles skip onboarding; companions, conversations, model pins and
   settings are retained.

## Upgrading from v0.4.x

1. **Back up first.** In Juno, open **Settings → Backups → Export full backup**,
   or quit Juno and copy `%USERPROFILE%\.juno` to a protected folder.
2. Close Juno completely.
3. Run the v0.5 installer. It upgrades in place and preserves companions,
   conversations, credentials, settings and work items.
4. Open Juno, let it finish starting, and confirm your provider connections and
   model pins.

If a conversation from an older profile does not open after the upgrade, see
`conversation-load-unavailable` in [KNOWN_ISSUES.md](https://github.com/tanishkfr/juno-beta/blob/main/KNOWN_ISSUES.md).

## Returning to an earlier build

An in-place downgrade is **not supported**. Data written by v0.5 may not be
understood by an older build.

1. Keep the upgraded data folder as it is; do not point an older build at it.
2. Restore your pre-upgrade backup into a fresh profile.
3. Reinstall the older installer and open the restored profile.

Back up the upgraded profile before attempting a rollback so the v0.5 state is
not lost.

## Uninstall

Use **Settings → Apps → Installed apps → Juno → Uninstall**, or the uninstaller in
`%LOCALAPPDATA%\Programs\juno`.

The uninstaller removes the program files. Your Juno data, conversations and
credentials are kept unless you explicitly remove them. See
[PRIVACY.md](PRIVACY.md) for the two data folders.

## Updates

Updates are manual in this beta. Juno may show a signed release announcement and
open its approved download page; it does not download or run an installer. See
[SECURITY.md](https://github.com/tanishkfr/juno-beta/blob/main/SECURITY.md).

The in-app announcement feed is not yet pointed at v0.5, so check the
[releases page](https://github.com/tanishkfr/juno-beta/releases) for new builds.

## Troubleshooting

| Symptom | What to try |
|---|---|
| “Windows protected your PC” | Verify the SHA-256, then **More info → Run anyway**. Do not disable security controls. |
| The installer is blocked by policy | Stop and contact your administrator. Do not bypass application control. |
| Juno opens to “Your workspace is unavailable” | Choose another companion or start a new chat. If it persists for a thread you need, see `conversation-load-unavailable` in [KNOWN_ISSUES.md](https://github.com/tanishkfr/juno-beta/blob/main/KNOWN_ISSUES.md). |
| Code is unavailable | Confirm the external OMP runtime is installed and authenticated, then check the Code model catalogue in Settings. |
| A provider is “connected” but no models appear | Refresh or reconnect the provider account; ChatGPT-plan catalogues are account-scoped. |
| A saved model will not run | The provider may have retired it. Pick a currently offered model; Juno will not silently substitute one. |

For anything else, use [FEEDBACK.md](FEEDBACK.md).
