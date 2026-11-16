# Installing Juno v0.5.1 Beta

Version `0.5.1-rc.1` · Windows 11 x64 · Unsigned installer · Manual updates

This guide covers installing, upgrading and uninstalling **Juno v0.5.1 Beta**. If something does
not match what you see, check [KNOWN_ISSUES.md](KNOWN_ISSUES.md) and the
[releases page](https://github.com/tanishkfr/juno-beta/releases).

## Requirements

- **Windows 11 x64.** Windows 10, Windows on ARM64, 32-bit Windows, macOS and Linux are not
  qualified for this beta.
- **A supported provider account** for external models. Juno does not include model capacity,
  subscriptions or quota.
- **Network access** for provider calls and optional runtime downloads.
- **Disk space.** The installer is 261,849,280 bytes (249.7 MiB); the installed application and
  bundled runtimes need additional space.
- **No administrator rights required.** The installer is per-user.
- **OMP is required for Code execution.** Boreal, Ariadne and Codex are bundled; OMP is not.

## Download

One installer is published for this release:

| File | Size |
|---|---:|
| `juno-0.5.1-rc.1-setup.exe` | 261,849,280 bytes |

Download it and `SHA256SUMS.txt` from the official release:

<https://github.com/tanishkfr/juno-beta/releases/tag/v0.5.1-rc.1>

That release page is the only official source. Do not use third-party mirrors or repacks.

## Verify before running

```powershell
Get-FileHash .\juno-0.5.1-rc.1-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected:

```text
A4375A29888956BE688ADB1BC714A10D2F84B04BCB349676ABCA9B0CED3B09BF  juno-0.5.1-rc.1-setup.exe
```

If the hash does not match, delete the file and download it again.

## Unsigned installer

The installer is **not code-signed**.

- Authenticode: `NotSigned`; no verified publisher and no SmartScreen reputation.
- Windows may show **Unknown Publisher** or **Windows protected your PC**.
- If SmartScreen appears, choose **More info**, confirm the file name, then **Run anyway** — only
  after the SHA-256 matches.
- Do not disable Microsoft Defender, SmartScreen, Smart App Control or antivirus.
- Managed PCs may block unsigned installers by policy. If you cannot proceed safely, stop.

The checksum proves integrity, not who built the file.

## New installation

1. Close any running Juno window.
2. Run the installer.
3. It installs in `%LOCALAPPDATA%\Programs\juno`, creates a **Juno** Start menu entry and a
   desktop shortcut, and registers **Juno** in **Settings → Apps → Installed apps**.
4. It does not launch Juno automatically.
5. Open Juno from the Start menu.

## Upgrade from v0.5.0

1. Keep a copy of your Juno workspace if you want a rollback path.
2. Close Juno.
3. Verify the v0.5.1 checksum.
4. Run the installer. It installs in place and preserves companions, conversations, provider
   settings, model selections, Mission/Code history and preferences.
5. Reopen Juno and confirm your companions and conversations are present.
6. Upgrade every Windows account that runs v0.5.0; the security fix protects the installed app.

There is no in-place downgrade. Restore a pre-upgrade backup into a fresh profile if you need to
return to an older build.

## First run and providers

1. Complete onboarding: profile, starting companion, optional capabilities.
2. Connect at least one provider in **Settings → Providers**.
3. Provider accounts, subscriptions, quotas and network access are your responsibility.
4. For ChatGPT-plan Codex, use the official Codex sign-in. Juno does not redirect it to a
   billable API key.
5. The browser engine, Android platform tools, cloudflared and the Whisper model are optional
   downloads where applicable.
6. Code execution additionally needs the external OMP runtime.

## Updates

Updates are **manual**. Juno does not download or install an update automatically. The signed
update announcement feed still describes `0.4.2-rc.3`; v0.5.1 is not announced in-app. Check the
release page and `https://juno.tanishk.me` for newer builds.

## Uninstall

Use **Settings → Apps → Installed apps → Juno → Uninstall**, or the uninstaller in the install
folder. Uninstalling removes the application and registration. Juno-owned profile data under
`%APPDATA%\Juno` and `%USERPROFILE%\.juno` is separate; remove it only if you intend to delete
your local workspace. Back up first.
