# Security and integrity — Juno v0.4.2 Beta

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
| Compact (recommended) | `juno-0.4.2-setup.exe` | 252,282,304 | `4AB457A97C0FB768768720ADCC7C9AF4BC5899FEF5D2D070D15176C51AA5522B` |
| Full/offline | `juno-0.4.2-full-setup.exe` | 488,599,330 | `8F73FE74E983AC217BFC15F4C71B34B3A72DAC2072617A2AC497A328C126F278` |

Verify:

```powershell
Get-FileHash .\juno-0.4.2-setup.exe -Algorithm SHA256
Get-FileHash .\juno-0.4.2-full-setup.exe -Algorithm SHA256
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
  `electron-updater` is not pointed at a live automatic-install feed; the
  packaged `app-update.yml` uses the reserved host `updates.invalid`.
- In manual mode the updater announces an available release and opens the
  release page. It does not fetch the installer.
- The in-app **Verify downloaded installer** action hashes a file you selected
  and compares it with a checksum file you selected. It refuses a malformed
  file, a checksum mismatch, an unknown channel and an unapproved downgrade.
- The signed automatic-installer upgrade path is **not qualified** and must not
  be represented as working. The announcement feed is not an automatic updater.

## Runtime and data handling

- The desktop server listens on loopback only. Remote access requires an
  explicit action and is not started by default.
- Provider credentials are stored through the Windows credential store and are
  write-only through the product UI.
- Optional browser and Whisper downloads are pinned by size and SHA-256 and are
  verified before use. Android tools and cloudflared use the same pinned
  download contract.
- No API keys, OAuth tokens, private developer paths or `.env` files are
  packaged. The packaged tree was scanned for token shapes, private-key
  markers, development paths and test endpoints.
- The public distribution repository contains only release documentation and
  metadata. The application source remains private.
- Third-party licence and notice files are shipped in `resources/licenses/`,
  including the Apache-2.0 product licence, `NOTICE`,
  `THIRD-PARTY-NOTICES.md`, Electron/Chromium notices, and the licences for the
  bundled browser, CUA driver, Codex runtime, Boreal and Whisper components.

## Reporting a vulnerability

Do not open a public issue with exploit details. Contact the maintainer through
the repository’s private security reporting channel, or use the feedback route
in **Settings > Help & feedback** and mark the report as security-sensitive.
Include the Juno version, Windows version, reproduction steps and impact.
Never include live credentials, tokens or private user data in a report.
