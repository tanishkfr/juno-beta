# Installing Juno v0.4.0 Beta

This guide covers the Windows x64 installers for **Juno v0.4.0 Beta —
Intelligence & Efficiency**.

## Requirements

- **Windows 11 x64.** Windows 11 is the qualified platform. Windows 10, macOS,
  Linux, ARM64 and 32-bit Windows are not qualified for this Beta.
- **A supported provider account** for external models. Juno does not include
  model capacity, subscriptions or quota.
- **Network access** for provider calls and for the optional browser/Whisper
  downloads in the compact build.
- **Disk space:** about 1.1 GB for the compact application, or about 1.6 GB if
  you install both optional assets later. The full/offline variant needs about
  1.5 GB. Leave additional space for projects, generated files and backups.
- **No administrator rights required.** The installer is per-user.

## Choose a download

| Variant | File | Size | Notes |
|---|---|---:|---|
| Compact (recommended) | `juno-0.4.0-setup.exe` | 271,652,163 B | Omits the browser engine and Whisper weights; installs them on request. |
| Full/offline | `juno-0.4.0-full-setup.exe` | 488,536,955 B | Includes the pinned browser engine and Whisper base.en model. External providers still need the internet. |

Both variants contain the same application code. The full variant only adds the
two large optional runtime assets.

## Download and verify

Download the installer and `SHA256SUMS.txt` from the official release:

<https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.0>

In PowerShell, from the download folder:

```powershell
Get-FileHash .\juno-0.4.0-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

For the full variant:

```powershell
Get-FileHash .\juno-0.4.0-full-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected SHA-256:

```text
4af07ecd32f8769524a7a72e027930e85cf793b46c23e1ab49c7305877be2942  juno-0.4.0-setup.exe
554ca46e69903e44dbad1aecb273737522b6c89cd6da0412fc0985f19319bbe8  juno-0.4.0-full-setup.exe
```

The hash is not case-sensitive. If it does not match, stop. Delete the file and
download it again. Do not install a file whose provenance you cannot verify.

`SHA256SUMS.txt` is a standard GNU checksum file: one
`<64-character-lowercase-hash><two spaces><exact filename>` record per line,
UTF-8 without a byte-order mark, LF line endings, and no extra fields. File
sizes are recorded in `artifacts.json`. On Linux, WSL, macOS or Git Bash, put
both installers and `SHA256SUMS.txt` in one folder and run:

```sh
sha256sum --check SHA256SUMS.txt
```

The v0.4.0 Git tag's automatically generated source archives are a historical
snapshot of the repository at release time. The release asset and `main` carry
the corrected checksum file; neither installer binary changed.

## Unsigned installer

The installer is **not code-signed**.

- Windows may show **Unknown Publisher** or “Windows protected your PC”
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

## Install

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

## First run

1. Complete onboarding: display name, starting companion, optional provider
   connection, appearance and privacy.
2. No Juno account is required. Storage is local-first.
3. Connect a provider you have an account for. Credentials are stored through
   the Windows credential store; Juno reports whether a credential is
   configured, never its value.
4. Run a short Bot Mode question.
5. Optional: open **Code**, choose a disposable project folder, and try a small
   edit.
6. Optional: install the browser engine or the local Whisper model from the
   relevant settings surface. Neither downloads during ordinary startup.

## Optional runtime downloads

### Browser automation

The compact installer does not include the browser engine. Installing it
downloads the pinned agent-browser binary and Chrome for Testing:

- about **160 MB** download;
- about **450 MB** on disk;
- verified by size and SHA-256 before use.

The full/offline variant includes the engine, so no download is needed for
browser automation.

### Local Whisper

The compact installer includes the Whisper engine but not the weights.

- The model is `ggml-base.en.bin`, **147,964,211 bytes**, SHA-256
  `a03779c86df3323075f5e796cb2ce5029f00ec8869eee3fdfb897afe36c6d002`.
- Juno downloads it only when you ask, verifies the size and hash, and keeps it
  under `%APPDATA%\Juno\optional-assets`.
- **System.Speech works immediately** and remains the fallback. You do not need
  the Whisper model to use speech output.

## Upgrade from Juno Beta 0.3

The public Beta 0.3 line used versions `1.0.0-rc.17` to `1.0.0-rc.21`. Version
`0.4.0` restarts the public version number.

### Supported manual path

A direct manual upgrade from `1.0.0-rc.18` to `0.4.0` was tested with data
preservation. The installer uses the same identity as Beta 0.3:

- appId `com.agent.app`;
- product name `Juno`;
- install directory `%LOCALAPPDATA%\Programs\juno`;
- data root `%USERPROFILE%\.juno`;
- Electron user data `%APPDATA%\Juno`.

The installer upgrades in place. It does not create a second copy.

### Before upgrading

1. Close Juno completely, including the tray icon.
2. Back up:
   - `%USERPROFILE%\.juno` (conversations, bots, memory, routines, work items);
   - `%APPDATA%\Juno` (credentials, window state, local settings);
   - the previous installer (`juno-1.0.0-rc.18-setup.exe` or
     `juno-1.0.0-rc.21-setup.exe`) for rollback.
3. Keep the backup until the new version has opened, shown your bots and
   conversations, and completed a short provider turn.

### What is preserved

The tested upgrade preserved:

- bots and conversations;
- work items and research records;
- provider configuration and credentials;
- settings and memory;
- SQLite integrity (`PRAGMA integrity_check = ok` for the tested databases).

### What is not supported

- The **signed automatic-update bridge** from `1.0.0-rc` to `0.4.0` is not
  qualified. Do not wait for an in-app automatic update. Download and run the
  installer manually.
- A downgrade from `0.4.0` back to Beta 0.3 is possible by running the old
  installer, but data written by `0.4.0` may not be understood by the older
  build. Back up first.
- In-app “Verify downloaded installer” accepts the 0.4.0 installer and the
  historical `1.0.0-rc` line. It still refuses arbitrary downgrades and
  cross-channel files.

## Uninstall and data preservation

1. Close Juno.
2. Open **Settings > Apps > Installed apps**, find **Juno**, and choose
   **Uninstall**.
3. The uninstaller removes the application directory and the Windows uninstall
   entry. It also removes the `juno://` handler and the app's notification
   registration.
4. It **does not delete**:
   - `%USERPROFILE%\.juno`;
   - `%APPDATA%\Juno`;
   - optional Whisper/browser assets under `%APPDATA%\Juno`.
5. Reinstalling Juno detects the existing data and optional assets.

To remove all local data, uninstall Juno and then delete those two folders
manually. Export anything you need first.

## Rollback

Reinstall the previous Beta 0.3 installer (`1.0.0-rc.18` or `1.0.0-rc.21`)
over `0.4.0`. Because the identity and install directory are unchanged, this is
an in-place replacement. Keep a backup of `%USERPROFILE%\.juno` and
`%APPDATA%\Juno` in case the older build cannot read newer data.

## Troubleshooting

**“Windows protected your PC”**
: Verify the SHA-256 first. Choose **More info > Run anyway** only if it
matches. Do not disable security controls.

**The installer is blocked by your organization**
: Stop. Ask your administrator. Juno cannot bypass an enterprise application
control policy.

**Juno opens but no model is available**
: Connect a provider in setup or **Settings > Providers**. Check the provider's
dashboard for subscription, quota and network requirements.

**Browser automation says the runtime is missing**
: Use the install action in Browser settings. It downloads the pinned engine.
The full/offline installer includes it.

**Speech uses the robotic voice**
: System.Speech is the fallback. Install the optional Whisper model in Speech
settings for local Whisper transcription. Whisper is speech-to-text; spoken
output still uses the Windows voice.

**The app does not start after an abrupt shutdown**
: Launch it again. The next start clears a stale data-directory lease. If it
still fails, close all Juno processes, keep the data folders, and report the
exact error.

**You need to report a problem**
: Use **Settings > Help & feedback > Report a bug**, or open an issue at
<https://github.com/tanishkfr/juno-beta/issues>. Never include API keys,
tokens, cookies or private documents.
