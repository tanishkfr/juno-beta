# Installing Juno v0.4.1 Beta

This guide covers the Windows x64 installers for **Juno v0.4.1 Beta — Unified
Agent Runtime**.

## Requirements

- **Windows 11 x64.** Windows 11 is the qualified platform. Windows 10, macOS,
  Linux, ARM64 and 32-bit Windows are not qualified for this Beta.
- **A supported provider account** for external models. Juno does not include
  model capacity, subscriptions or quota.
- **Network access** for provider calls and for the optional browser/Whisper
  downloads in the compact build.
- **Disk space:** about 1.05 GB for the compact application, or about 1.50 GB
  for the full/offline variant. Leave additional space for projects, generated
  files and backups.
- **No administrator rights required.** The installer is per-user.

## Choose a download

| Variant | File | Size | Notes |
|---|---|---:|---|
| Compact (recommended) | `juno-0.4.1-setup.exe` | 271,664,867 B | Omits the browser engine and Whisper weights; installs them on request. |
| Full/offline | `juno-0.4.1-full-setup.exe` | 488,550,122 B | Includes the pinned browser engine and Whisper base.en model. External providers still need the internet. |

Both variants contain the same application code. The full variant only adds the
two large optional runtime assets.

## Download and verify

Download the installer and `SHA256SUMS.txt` from the official release:

<https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.1>

In PowerShell, from the download folder:

```powershell
Get-FileHash .\juno-0.4.1-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

For the full variant:

```powershell
Get-FileHash .\juno-0.4.1-full-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected SHA-256:

```text
3b6b3ef3ec870ca779e1a7b623a3d970d468729f0b9bf2608b171f2400233ebd  juno-0.4.1-setup.exe
c64a3441209becb10a569498c8fdf403c41592ee5779880b98b8576baa8cd864  juno-0.4.1-full-setup.exe
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

Provider accounts, subscriptions, quotas and network access are independent of
Juno. A provider may retire, rename or restrict a model; an explicit stale pin
is refused rather than silently replaced.

## Optional browser and Whisper assets

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

## Upgrade from v0.4.0

Installing v0.4.1 over v0.4.0 is an in-place upgrade. The installer uses the
same identity as v0.4.0:

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
   - the v0.4.0 installer for rollback.
3. Keep the backup until the new version has opened, shown your bots and
   conversations, and completed a short provider turn.

### What is preserved

The production upgrade test preserved:

- 17 existing bots;
- existing configuration;
- 25 work items;
- conversation and user data across install, uninstall and reinstall;
- provider configuration and credentials;
- memory, routines and settings.

The v0.4.1 task-runtime tables are additive. Existing v0.4.0 data opens without
a destructive migration.

## Where your data lives

- Data root: `%USERPROFILE%\.juno`
- Desktop profile: `%APPDATA%\Juno`
- Credentials: `%APPDATA%\Juno\credentials.bin` (OS-protected)

The installer does not delete bots, conversations, work items, approvals,
memory, routines, usage or credentials. A clean backup is still recommended
before any upgrade.

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

## Rollback to v0.4.0

Back up first. Rollback is supported to v0.4.0 for this release, but unrestricted
compatibility with future schema versions is not promised.

1. Close Juno and confirm no Juno process is running.
2. Copy `%USERPROFILE%\.juno` and `%APPDATA%\Juno` to a safe location.
3. Keep the v0.4.0 installer and checksum from the preserved v0.4.0 release:
   <https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.0>
4. Install the v0.4.0 installer over v0.4.1.
5. Launch Juno and verify your bots and conversations.

A v0.4.0 build opens the newer work-item database with its documented
newer-schema tolerance. It ignores the v0.4.1 runtime/call/event tables and
rewrites the schema-version metadata to 5. All tables and rows remain;
reinstalling v0.4.1 restores schema 7. This is a metadata downgrade, not data
loss. Restore the backup only if the rollback install did not preserve your
data.

## Updates

Updates are manual in this Beta. Juno does not download or run installers
automatically.

- The packaged `app-update.yml` points at the reserved host
  `updates.invalid`, so there is no live automatic-install feed.
- Juno may check Ed25519-signed release metadata and show release notes.
- The feed is announcement-only. It never downloads or executes an installer.
- The signed automatic-installer upgrade path is not qualified.

## Troubleshooting

**Windows protected your PC**
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
