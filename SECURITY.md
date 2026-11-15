# Security and integrity — Juno v0.5 Beta

Version `0.5.0-rc.1` · Windows 11 x64 · Unsigned · Manual updates

## Signing status

**The Windows installer is unsigned.**

- Authenticode: `NotSigned`
- Publisher: no verified publisher identity
- SmartScreen: no publisher reputation; Windows may warn or block

This is an explicitly accepted limitation of the public beta. Do not describe the
installer as signed, trusted by SmartScreen, or publisher-verified.

## Official artifact

| File | Bytes | SHA-256 |
|---|---:|---|
| `juno-0.5.0-rc.1-setup.exe` | 261,843,896 | `B8C931EC42D7892B5FA8E64781220A3A270895AD586636801E53C1452CEBB5C6` |

Verify:

```powershell
Get-FileHash .\juno-0.5.0-rc.1-setup.exe -Algorithm SHA256
```

Download only from:

<https://github.com/tanishkfr/juno-beta/releases>

The release page is the only official source. Do not use third-party mirrors,
repacks or “fixed” installers.

## What the checksum proves

SHA-256 proves that the file you downloaded is byte-for-byte the file named in the
release checksum. It does **not** prove who built it or that a publisher vouches
for it. The release page and the checksum file are hosted by the same publisher;
neither is a substitute for Authenticode.

## Windows security

- Do not disable Microsoft Defender, SmartScreen, Smart App Control, antivirus,
  firewall or any other Windows security control.
- If SmartScreen offers **More info → Run anyway**, use it only after the checksum
  matches.
- If your organization blocks unsigned installers, stop. Do not attempt to bypass
  application control, WDAC, AppLocker or endpoint protection.
- Report the exact Windows message rather than working around a security block.

## Update behaviour

- Installation and updates are **manual** in this beta.
- Juno may check an Ed25519-signed release metadata feed and show the released
  version and notes. Metadata is verified with a public key pinned in the build.
- Juno **never downloads or executes an installer** from that feed.
  `electron-updater` is not pointed at a live automatic-install feed; the
  packaged `app-update.yml` uses the reserved host `updates.invalid`.
- In manual mode the updater announces an available release and opens the approved
  release page. It does not fetch the installer.
- A signed announcement may carry its own HTTPS download page. It is validated
  before it is opened; invalid signatures and non-HTTPS or credential-bearing
  URLs are refused, and the build’s trusted page remains the fallback.
- The in-app **Verify downloaded installer** action hashes a file you select and
  compares it with a checksum file you select. It refuses a malformed file, a
  checksum mismatch, an unknown channel and an unapproved downgrade.
- The signed automatic-installer upgrade path is **not qualified** and must not be
  represented as working. The announcement feed is not an automatic updater.

## Runtime and data handling

- The desktop server listens on loopback only. Remote access requires an explicit
  action and is not started by default.
- Provider credentials are stored through the Windows credential store and are
  write-only through the product UI.
- Optional browser, speech, Android and cloudflared assets are pinned by size and
  SHA-256 and verified before use.
- No API keys, OAuth tokens, private developer paths or `.env` files are packaged.
  The packaged tree is scanned for token shapes, private-key markers, development
  paths and test endpoints.
- The public distribution repository contains only release documentation and
  metadata. The application source remains private.
- Third-party licence and notice files ship in `resources/licenses/`, including
  the Apache-2.0 product licence, `NOTICE`, `THIRD-PARTY-NOTICES.md`,
  Electron/Chromium notices, and the licences for the bundled browser, CUA driver,
  Codex runtime, Boreal and speech components.

## Permission boundaries

Code and Mission work is authorized per task. File writes, commands and approvals
are scoped to what the task authorized; a read-only Code run fails validation if it
changed anything, and a Code change is staged for review before it is applied.
Ariadne verifies declared checks; it is not a general proof of every model claim.

## Reporting a vulnerability

Please report security problems privately. Do not open a public issue with exploit
details.

1. **Email `madebytanishk@gmail.com`** with:
   - the Juno version (`0.5.0-rc.1`) and Windows build;
   - the affected area (installer, local server, permissions, provider handling,
     update metadata, Code/Mission boundary);
   - reproduction steps and impact;
   - whether the issue is already public.
2. Alternatively use GitHub’s private vulnerability reporting on this repository
   if it is enabled for your account.
3. **Never include** live API keys, tokens, cookies, credentials, personal data or
   private documents. Redact paths and screenshots.

What to expect: an acknowledgement when the report is reviewed, a request for a
minimal reproduction if needed, and credit if you want it. This is a public beta
with no guaranteed response time or bounty program.

Please do not test against other people’s data, and do not run destructive tests
on work you cannot lose.
