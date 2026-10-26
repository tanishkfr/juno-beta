# Installing Juno Beta 0.3 (Final)

This guide covers the Windows installer for `1.0.0-rc.18`.

## Requirements

- **Windows 11 x64.** Windows 10, macOS and Linux are not qualified for this Beta.
- **A GitHub account with read access to this private repository.** Ask the owner for an invitation. A copied release link will not work without access.
- **A supported provider account.** Command Code is the best-qualified route in this Beta; other providers may be visible but are less tested.
- **About 1 GB free disk space** for the application and generated work.
- **Optional:** Microsoft PowerPoint for slide previews and PDF export from generated presentations.
- **Optional:** FFmpeg on `PATH` for procedural video generation.

## Download

Open the current release:

<https://github.com/tanishkfr/juno-beta/releases/tag/v1.0.0-rc.18>

Download:

- `juno-1.0.0-rc.18-setup.exe`, the installer.
- `SHA256SUMS.txt`, the checksum file for this release.

The release is a regular private release on GitHub. The version still carries the `rc` suffix because this is a Beta release candidate, not a claim of 1.0 product maturity.

## Verify the download

In PowerShell, from the download folder:

```powershell
Get-FileHash .\juno-1.0.0-rc.18-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected file size: `391,808,044` bytes.

Expected SHA-256:

```text
D28E79636D19BAABC7CC9DA8D926519211AFF4F3BE0335641865A768404AC2A0
```

The hash is not case-sensitive. If it differs from `SHA256SUMS.txt`, stop. Delete the file and download it again. Do not install a file that does not match.

## Unsigned installer

The installer is **not code-signed**. Windows SmartScreen may show "Windows protected your PC", or the publisher may appear as **Unknown publisher**.

- Continue only if the SHA-256 matches the value above.
- If SmartScreen appears, choose **More info**, confirm the app name, then choose **Run anyway**.
- Do not disable Windows Defender, SmartScreen, Smart App Control or any other security control.
- If Windows blocks the installer and you cannot proceed safely, stop and report the exact message. Do not work around a security block.

SmartScreen, Unknown Publisher and the absence of a signature are expected for this Beta. They do not mean the download is corrupted. The checksum is the integrity check; it is not a publisher identity check.

## Install

The rc.18 installer is a one-click, per-user NSIS installation.

1. Run `juno-1.0.0-rc.18-setup.exe`.
2. The installer places the application in `%LOCALAPPDATA%\Programs\juno`.
3. It creates a **Juno** Start menu entry and a desktop shortcut.
4. It does not launch Juno automatically. Open Juno from the shortcut.
5. Windows registers **Juno** in **Settings > Apps > Installed apps** with an uninstaller.

The installation uses the same Windows application identity as earlier Juno Beta builds, so the installer is configured as an **in-place upgrade** of an existing Juno Beta. It does not install side by side, and it does not create a second Juno installation.

### Important verification note

The rc.18 NSIS installer has **not** been executed in a fresh, independent Windows environment. The extracted packaged application was tested successfully, including onboarding, reporting, updates and restart behavior. A complete rc.18 install, first launch from the installed location, and uninstall journey still needs independent confirmation.

If the installer fails, stops early or leaves a broken shortcut, report it through the feedback channel with the exact error text and your Windows version. Do not repeatedly reinstall over a failing installation.

## First run

1. Open Juno from the Start menu or desktop shortcut.
2. Complete onboarding: display name, starting companion, optional provider connection, appearance and privacy.
3. No Juno account is required. The app is local-first.
4. Connect a provider you have an account for. Provider keys are stored through the operating system credential store.
5. Take the optional product tour. It can be replayed later from **Settings > Help & feedback**.
6. Open **Settings > General** to confirm the version shows `Juno Beta 0.3` and `1.0.0-rc.18`.

## Connecting a provider

Open **Settings > Providers** (or the provider step in setup) and connect a supported route. Command Code is the best-qualified route in this Beta; other routes may be present but are less tested.

A provider key is write-only through the app: Juno reports whether a credential is configured, never the value. Provider usage, limits and billing are governed by your provider account, not by Juno.

If a provider shows an authentication or connection error, check the provider's own dashboard and your network before reporting a Juno bug. Include the exact Juno error code and the provider name, but never the key.

## Upgrading from an earlier Beta

- rc.18 installs **in place** over an existing Juno Beta. Bots, conversations, settings and credentials are preserved by the upgrade.
- Testers on rc.17 or earlier must install rc.18 manually. Those builds contain no update feed and cannot discover this release.
- After rc.18, future releases can be discovered through the signed update feed. Installation stays manual because the installer is unsigned.
- Keep the previous installer until the new build opens cleanly.

## Local data and rollback

Juno keeps data in two places:

```text
%APPDATA%\Juno     desktop state, logs, encrypted credentials, crash records
%USERPROFILE%\.juno  bots, conversations, memory, routines, artifacts
```

Back up both folders before a significant upgrade if the work matters to you. The folders contain private conversations and credentials; store any backup securely.

To roll back, close Juno and run the previous installer again. The install is in place, so the older application replaces the newer one. Your local data is not deleted by the installer. A downgrade is not formally qualified: data written by a newer build may not be understood by an older one. Keep a backup and report any downgrade problem.

## Troubleshooting

- **SmartScreen or Unknown Publisher:** expected for the unsigned Beta. Verify the SHA-256 before continuing.
- **The installer does not start:** confirm Windows 11 x64, that the file is not blocked by policy, and that you have free disk space. Report the exact message; do not disable security controls.
- **Juno does not start:** check `%APPDATA%\Juno\logs\server.log` and `%APPDATA%\Juno\logs\desktop-crashes.log`. Remove API keys, private paths and personal content before sharing.
- **Provider not ready:** open **Settings > Providers** and confirm the connection. A key cannot be read back; re-enter it if the provider revoked it.
- **Code workspace unavailable:** check the Code availability row above the composer in Code mode and the runtime status it reports. Report the exact status text if it stays unavailable.
- **Slide preview or PDF export missing:** install Microsoft PowerPoint, or download the editable PPTX and open it directly.
- **Video generation unavailable:** install FFmpeg and ensure `ffmpeg` is on `PATH`.
- **Juno keeps running after the window closes:** this is the background host setting. Use the tray menu to quit, or turn off "Keep Juno running when I close the window" in Settings.

## Uninstall

Use **Settings > Apps > Installed apps > Juno > Uninstall**, or run:

```text
%LOCALAPPDATA%\Programs\juno\Uninstall Juno.exe
```

Uninstall removes the application, shortcuts and its Windows registration.

Uninstall does **not** delete your local data by default:

- `%APPDATA%\Juno`
- `%USERPROFILE%\.juno`

Delete those folders manually only if you intend to remove all local Juno data. Deletion is permanent. Back up anything you need first.

## Getting help

Use **Settings > Help & feedback > Report a bug** and choose **Open Email Draft**, or open an issue in this repository. See [FEEDBACK.md](FEEDBACK.md) for the details that make a report useful and for the privacy rules.
