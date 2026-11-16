# Juno v0.5.1 Beta — Security & Reliability

**Public beta · Windows 11 x64 · Version 0.5.1 · Unsigned installer · Manual updates**

Juno v0.5.1 is a maintenance release for the v0.5 public beta. It keeps the product and provider
routes from v0.5.0 and focuses on security, reliability and clearer setup.

> The public release is titled **v0.5.1**. The installed application reports its internal build
> version as **`0.5.1-rc.1`**. This is a beta, not a stable general-availability release.

## Download

| File | Size |
|---|---:|
| `juno-0.5.1-rc.1-setup.exe` | 261,849,280 bytes (249.7 MiB) |

Download the installer and `SHA256SUMS.txt` from:

https://github.com/tanishkfr/juno-beta/releases/tag/v0.5.1-rc.1

That release page is the only official source. Do not use third-party mirrors or repacks.

## Verify before installing

```powershell
Get-FileHash .\juno-0.5.1-rc.1-setup.exe -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

Expected:

```text
A4375A29888956BE688ADB1BC714A10D2F84B04BCB349676ABCA9B0CED3B09BF  juno-0.5.1-rc.1-setup.exe
```

The installer is **unsigned**. Windows may show Unknown Publisher or SmartScreen. Continue only
after the SHA-256 matches. Do not disable Windows security protections.

## Security

- **Local data is isolated between Windows accounts.** v0.5.0 could expose some local Juno data
  to another Windows user on the same PC under specific local conditions. v0.5.1 requires the
  desktop capability, or a paired session, for data routes. Health and static identity routes
  remain public.
- **Existing v0.5.0 beta users should upgrade.** The fix protects the installed app; the older
  build remains exposed until it is replaced.
- **Port conflicts fall back cleanly.** Juno checks a loopback port before starting its server
  and uses the next port instead of failing with an address-in-use error.

## Reliability

- **OpenCode works after a managed install.** Juno installs the 2.x `@opencode/cli` package,
  discovers models without restarting, and explains when a free catalogue is outside the managed
  Bot chain.
- **Provider cards remain available.** Configured providers no longer disappear while the
  optional catalogue is loading, and the list survives restart.
- **ChatGPT state and model selection are clearer.** A single eligible model saves correctly,
  a valid connection is not shown as signed out after restart, and quota prose is reported as a
  usage limit rather than an authentication failure.
- **Reasoning alone is not an answer.** A provider that ends with reasoning and no answer text
  now reports a failed turn.
- **Stale conversations recover safely.** A remembered thread that no longer exists no longer
  strands the workspace; Juno returns to the companion's valid conversation and keeps the stored
  transcript.
- **Conversation and model state persist after restart.**

## Usability

- Onboarding now explains when a provider is required, what can be skipped, and what remains
  usable without one.
- Missing runtimes and unconnected providers read as setup states, not red failures.
- Coding and Computer control status reflect the actual runtime and capability state.
- Companion selection uses a radio group with arrow-key navigation.
- Settings navigation, provider rows and selected states are clearer; the right-side workspace
  panel slides in Bot and Code modes and sits closer to the conversation.
- The Code panel's first tool tab has breathing room from its rounded frame.

## Requirements and disclosures

- **Windows 11 x64** is the qualified platform. Windows 10, Windows on ARM64, 32-bit Windows,
  macOS and Linux are not qualified for this beta.
- **A provider account is required for model access.** Provider accounts, subscriptions, network
  access and quota are your responsibility. Juno does not include model capacity.
- **Code work needs the external OMP runtime.** Juno bundles its Code coordinator (Boreal), the
  Ariadne verifier and the Codex runtime, but not OMP.
- **Updates are manual.** Juno does not download or run installers for you. The signed update
  announcement feed still describes the previous beta (0.4.2-rc.3); check this release page and
  the website for newer builds.
- **No in-app v0.5.1 announcement is expected** because the production update-signing key is not
  available for this release.
- **Optional downloads:** the browser engine, Android platform tools, cloudflared and the Whisper
  model are installed on request where applicable.
- **Unsigned installer:** no Authenticode publisher identity and no SmartScreen reputation.
  SHA-256 proves integrity, not who built the file.

## Known issues

See [KNOWN_ISSUES.md](KNOWN_ISSUES.md) and the versioned registry at
[support/v0.5.1-rc.1/known-issues.json](support/v0.5.1-rc.1/known-issues.json).

Notable limitations: provider quota and availability are external; a clean Windows 11 VM run
was not part of this qualification; the installer is unsigned; v0.5.1 is manual-update only;
historical conversations without a durable companion association may need backup recovery.

## Upgrade from v0.5.0

1. Keep a copy of your existing Juno workspace if you want a rollback path.
2. Close Juno.
3. Verify the v0.5.1 SHA-256.
4. Run the installer. It installs in place, per user, and preserves companions, conversations,
   provider settings, model selections, Mission/Code history and preferences.
5. Reopen Juno and confirm your companions and conversations are present.
6. Review the security note and upgrade any other Windows account that runs v0.5.0.

There is no in-place downgrade. Restore a pre-upgrade backup into a fresh profile if you need to
return to an older build.
