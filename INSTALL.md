# Installing Juno Beta 0.1

## Requirements

- Windows 11 x64 (Windows 10 is not qualified for this Beta).
- A supported provider account. The Beta was qualified with **Command Code**; other provider rows
  may exist but are not all equally qualified.
- Optional: Microsoft PowerPoint for slide image previews / PDF export from generated decks.
- Optional: FFmpeg on `PATH` for procedural video generation.
- About 1 GB free disk space for the app and generated work.

## Download

From the private prerelease:

<https://github.com/tanishkfr/juno-beta/releases/latest>

Download:

- `juno-1.0.0-rc.7-setup.exe` — the installer.
- `SHA256SUMS.txt` — checksums.

The release is marked **prerelease**. The asset must match the tested candidate byte-for-byte.

## Verify (recommended)

In PowerShell, from the download folder:

```powershell
Get-FileHash .\juno-1.0.0-rc.7-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected for this candidate:

```text
2209AD0A24D51743CB92FDD7AE34BF9BB60F2F648BE5F9E8BE564180B502D3EE  juno-1.0.0-rc.7-setup.exe
```

If the hashes differ, **do not install**. Report it through the feedback channel.

## Unsigned installer

The installer is **not code-signed**. No certificate was available for this Beta. Windows
SmartScreen may show "Windows protected your PC" or an "Unknown publisher" warning.

- If you trust this private Beta and the checksum matches, choose **More info** and then
  **Run anyway**.
- Do not disable Windows Defender, SmartScreen or any other security control.
- If Windows blocks installation and you cannot proceed safely, stop and report the exact message
  and a screenshot (with no personal data) through the feedback channel.

## Install

1. Run `juno-1.0.0-rc.7-setup.exe`.
2. The one-click installer installs per-user to:
   `%LOCALAPPDATA%\Programs\juno`
3. It creates a **Juno** Start menu shortcut and a desktop shortcut. It does not launch the app
   automatically; open it from the shortcut.
4. On first launch, complete onboarding. No Juno account is required. Connect a provider you have
   an account for.

## Uninstall

Use **Settings → Apps → Installed apps → Juno → Uninstall**, or run:

```text
%LOCALAPPDATA%\Programs\juno\Uninstall Juno.exe
```

Uninstall removes the application and shortcuts. It does **not** delete your Juno data by default:
desktop state stays under `%APPDATA%\Juno` and agents/conversations stay under `~/.juno`. Delete
those folders manually only if you intend to remove your local data.

## Updates

There is no auto-update channel in this private Beta. To move to a newer candidate, install the new
signed/unsigned installer from the release page. Do not install a build from an untrusted source.

## Troubleshooting

- **SmartScreen warning** — expected for an unsigned Beta; verify the SHA-256 first.
- **App does not start** — check `%APPDATA%\Juno\logs\server.log` and `desktop-crashes.log`.
  Remove API keys and personal data before sharing.
- **Provider not ready** — open Settings → Providers and confirm the key is connected. A key is
  write-only; Juno never displays it back.
- **Deck preview unavailable** — install Microsoft PowerPoint or use the Download button; the PPTX
  is still editable.
- **Video generation unavailable** — install FFmpeg and ensure `ffmpeg` is on `PATH`.
- **Background process** — closing the window can leave the host running by design. Use the tray's
  **Quit** to stop it, or turn off "Keep Juno running when I close the window" in Settings.
