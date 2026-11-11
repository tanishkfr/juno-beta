# Juno v0.4.2 Beta — Performance & Polish

**Public Beta · Windows 11 x64 · Version 0.4.2 · Unsigned installer · Manual updates**

Juno v0.4.2 is a performance and polish release. It keeps the provider routes,
Code execution boundary, Council policy, Ariadne verification and exact model
pins from v0.4.1. It is not a frontend rewrite and it does not remove Boreal,
Pi or OMP.

## Download

| Variant | File | Size |
|---|---|---:|
| **Compact (recommended)** | `juno-0.4.2-setup.exe` | 252,282,304 B |
| **Full/offline** | `juno-0.4.2-full-setup.exe` | 488,599,330 B |

The full variant includes the pinned browser engine, Whisper base.en model,
Android platform tools and cloudflared. External model providers still need
internet access, an account and quota.

## Verify before installing

```powershell
Get-FileHash .\juno-0.4.2-setup.exe -Algorithm SHA256
Get-FileHash .\juno-0.4.2-full-setup.exe -Algorithm SHA256
```

Expected:

```text
4ab457a97c0fb768768720adcc7c9af4bc5899fef5d2d070d15176c51aa5522b  juno-0.4.2-setup.exe
8f73fe74e983ac217bfc15f4c71b34b3a72dac2072617a2ac497a328c126f278  juno-0.4.2-full-setup.exe
```

The installer is **unsigned**. Windows may show Unknown Publisher or
SmartScreen. Continue only if the checksum matches. Do not disable Windows
security controls.

## Highlights

### Fewer reported input tokens

In the matched Phase 1 short-turn benchmark, Juno reported approximately
**80.5% fewer input tokens**. Task-aware tool exposure sends only the tools a
turn needs, and the direct-turn catalogue is smaller. This is a measured
benchmark result on that task shape. It does not mean every task, provider or
conversation will use 80.5% fewer tokens.

### Smaller and faster

- Compact installer: **271.7 MB → 252.3 MB**.
- Warm health median **3,253 ms**, first renderer body **6,479 ms**, and
  composer-ready **6,372 ms** on the tested Windows host.
- The renderer now reports shell-mounted, first-transcript and composer-ready
  marks, so startup claims reflect what you can actually use.

These are measurements from the qualification host, not guarantees.

### Modular optional runtimes

- Android platform tools and cloudflared are optional downloads with pinned
  versions, sizes and SHA-256 hashes. Install, verify, repair and remove them
  from Settings.
- Browser engine and Whisper remain optional in the compact variant and are
  included in the full/offline variant.
- Codex, Boreal/OMP and CUA remain bundled. They are not optional downloads.

### Onboarding and Settings

- Capability onboarding presents Chat, Coding, Browser, Computer control,
  Android devices, Local voice and Remote access with purpose, included or
  download size, and honest offline behaviour.
- A failed optional download is listed on the ready screen with Retry; it does
  not block setup.
- Runtimes & storage shows ready/attention counts, provider health, measured
  application/managed/optional/cache storage, accessible progress and safe
  removal confirmation.

### Code Mode correctness

- “Do not change README.md” no longer authorizes README.md as a writable target.
  A file named only to run (`node check.mjs`) is an input, not an editable
  target.
- Explicit content criteria (“containing exactly …”, “append a line …”, “two
  lines: the first line is …”) become deterministic checks over the staged
  workspace.
- A verified but unapplied change remains **staged**. Applying records
  completion; discarding or rolling back records cancellation. Failed staging
  or validation is reported as failed, never completed.
- The final Code message states whether the change is staged, could not be
  staged, or failed validation.

### Browser cleanup

- The model can close its own tab or browser session with
  `agent_browser_tab_close` / `agent_browser_close`. The close is scoped to the
  bot's isolated session; it cannot close your browser or another application's
  browser.
- A closed session is settled even when it never performed an action, so it
  cannot leave an agent-owned browser row behind.
- Cancellation and app exit release owned sessions.

### Installer identity and release safety

- Packaging uses named production and test profiles. App ID, product name,
  package/install directory, user-data directory, protocol, uninstall GUID,
  toast CLSID, update channel and executable are validated before and after
  packaging.
- A test installer cannot claim the production identity, and a production
  installer cannot be installed over a different identity.

### Preserved

- Codex ChatGPT-plan subscription route and exact model pins.
- Council planner/executor/reviewer policy and mandatory reviewer settlement.
- Ariadne as the independent Code verification authority.
- Existing task, approval, spend and capability boundaries.

## Compatibility

- Windows 11 x64 is the qualified platform.
- v0.4.2 upgrades v0.4.1 in place with the same application identity.
- The public v0.4.1 installer remains available for a manual rollback. Back up
  your data first. Rollback compatibility is not promised for future schema
  versions.
- Installation and updates are manual. Juno does not download or run an
  installer from the signed announcement feed.

## Known limitations

See [KNOWN_ISSUES.md](KNOWN_ISSUES.md). The main points are: unsigned
installers, manual updates, no enforceable universal spending hard cap, no
automatic safe idle retirement of Boreal/OMP or CUA, hardware-bound Android
qualification, no live microphone acceptance, and no public remote-access tunnel
exercise. External providers require their own accounts and subscriptions.
