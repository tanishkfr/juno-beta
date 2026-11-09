# Security and integrity — Juno v0.4.0 Beta

## Signing status

**The Windows installers are unsigned.**

- Authenticode: `NotSigned`
- Publisher: no verified publisher identity
- SmartScreen: no publisher reputation; Windows may warn or block

This is an explicitly accepted limitation of the public beta. Do not describe
the installer as signed, trusted by SmartScreen, or publisher-verified.

## Official artifacts

| Variant | File | Bytes | SHA-256 |
|---|---|---:|---|
| Compact (recommended) | `juno-0.4.0-setup.exe` | 271,652,163 | `4AF07ECD32F8769524A7A72E027930E85CF793B46C23E1AB49C7305877BE2942` |
| Full/offline | `juno-0.4.0-full-setup.exe` | 488,536,955 | `554CA46E69903E44DBAD1AECB273737522B6C89CD6DA0412FC0985F19319BBE8` |

Verify:

```powershell
Get-FileHash .\juno-0.4.0-setup.exe -Algorithm SHA256
Get-FileHash .\juno-0.4.0-full-setup.exe -Algorithm SHA256
```

Download only from:

<https://github.com/tanishkfr/juno-beta/releases>

Do not use third-party mirrors, repacks or “fixed” installers.

## What the checksum proves

SHA-256 proves that the file you downloaded is byte-for-byte the file named in
the release checksum. It does **not** prove who built it or that a publisher
vouches for it. The release page and the checksum file are hosted by the same
publisher; neither is a substitute for Authenticode.

## Windows security

- Do not disable Microsoft Defender, SmartScreen, Smart App Control,
  antivirus, firewall or any other Windows security control.
- If SmartScreen offers **More info > Run anyway**, use it only after the
  checksum matches.
- If your organization blocks unsigned installers, stop. Do not attempt to
  bypass application control, WDAC, AppLocker or endpoint protection.
- Report the exact Windows message rather than working around a security
  block.

## Update behavior

- Installation and updates are **manual** in this beta.
- Juno may check an Ed25519-signed release metadata feed and show the released
  version and notes. Metadata is verified with a public key pinned in the build.
- Juno **never downloads or executes an installer** from that feed.
  `electron-updater` is not pointed at a live automatic-install feed;
  the packaged `app-update.yml` uses the reserved host `updates.invalid`.
- The in-app **Verify downloaded installer** action hashes a file you selected
  and compares it with a checksum file you selected. It refuses a malformed
  file, a checksum mismatch, an unknown channel and an unapproved downgrade.
- The signed automatic-update bridge from the old `1.0.0-rc` line to `0.4.0`
  is **not qualified** and must not be represented as working.

## Runtime and data handling

- The desktop server listens on loopback only. Remote access requires an
  explicit action and is not started by default.
- Provider credentials are stored through the Windows credential store and are
  write-only through the product UI.
- Optional browser and Whisper downloads are pinned by size and SHA-256 and are
  verified before use.
- No API keys, OAuth tokens, private developer paths or `.env` files are
  packaged. The packaged tree was scanned for token shapes, private-key
  markers, development paths and test endpoints.
- Third-party licence and notice files are shipped in `resources/licenses/`,
  including the Apache-2.0 product licence, `NOTICE`,
  `THIRD-PARTY-NOTICES.md`, Electron/Chromium notices, and the licences for the
  bundled browser, CUA driver, Codex runtime, Boreal and Whisper components.

## Reporting a vulnerability

Do not open a public issue with exploit details. Contact the maintainer through
the repository's private security reporting channel, or use the feedback route
in **Settings > Help & feedback** and mark the report as security-sensitive.
Include the Juno version, Windows version, reproduction steps and impact.
Never include live credentials, tokens or private user data in a report.
