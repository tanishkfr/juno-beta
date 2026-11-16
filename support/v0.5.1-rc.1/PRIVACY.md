# Privacy — Juno v0.5.1 Beta

This page describes data handling for **Juno v0.5.1 Beta**, version `0.5.1-rc.1`. It is a plain
description of the beta implementation, not a legal privacy policy and not a substitute for your
AI provider's terms.

Juno is local-first, but not offline. It makes network requests when you use a provider, browser,
research, Code, or the update check.

## What stays on your computer

Juno stores its data in:

```text
%APPDATA%\Juno        desktop state, logs, crash records, encrypted credentials
%USERPROFILE%\.juno   companions, conversations, memory, routines, Missions, Code work and files
```

These folders can contain private conversations, prompts, results, project paths and Code diffs.
Treat them as private data. The local server listens on loopback only; paired/remote flows are
desktop-scoped for this beta.

v0.5.1 fixes an isolation issue in v0.5.0: another Windows user on the same PC could reach some
local Juno data under specific local conditions. v0.5.1 requires the desktop capability, or a
paired session, for local data routes. Health and static identity routes remain public. Existing
v0.5.0 installations remain exposed until upgraded.

## What leaves your computer

### AI providers

When you send a message, the prompt and the context needed for that turn go to the provider you
selected. That can include conversation history, selected files or excerpts, Code workspace
content, tool results and system instructions. The provider handles that data under its own terms,
retention policy and billing. Juno does not proxy provider traffic through an owner-operated
service.

### Code and Missions

Code runs through Juno's Code coordinator (Boreal) and the external OMP worker you installed.
Prompts, file excerpts and tool results needed for the run go to that worker's configured provider.
A Mission carries its authorized objective to the Code run.

### Tools and network access

If you authorize browser, research, computer or terminal tools, those tools can make network
requests and read or write files according to the permissions you granted. Those requests go to
the destinations involved, not to the Juno owner.

### Update metadata

Juno may request this public JSON file over HTTPS:

```text
https://tanishkfr.github.io/juno-update-feed/latest.juno.json
```

The request asks for release metadata only. It does not send conversations, account identifiers
or a Juno account identifier. GitHub Pages can see standard request information such as your IP
address and user agent. For v0.5.1 the feed still describes `0.4.2-rc.3`; no v0.5.1 in-app
announcement is expected.

### Crash records and feedback

Juno keeps local crash and error records under `%APPDATA%\Juno\diagnostics`. Nothing is uploaded
automatically. Bug reports are prepared locally and opened in your own mail app; nothing is sent
until you press Send. Diagnostics are optional and allowlisted. See [FEEDBACK.md](FEEDBACK.md).

## Credentials

Provider keys are stored in Juno's desktop data folder using the operating system's encrypted
credential store (`credentials.bin`). The app reports whether a credential is configured but does
not display the value back. A copied profile is only usable by the same Windows user and machine
credential context. Do not share your profile folder or paste keys into a report.

v0.5.1 moves an OpenAI-compatible provider key that v0.5.0 kept in plaintext configuration into
the encrypted credential store during upgrade.

## What Juno does not collect

Juno v0.5.1 has no product telemetry, analytics endpoint, advertising identifier or automatic
crash upload. It does not create a Juno account or require a cloud sign-in for the desktop app.
This does not cover providers, websites or the OMP worker you choose to use.
