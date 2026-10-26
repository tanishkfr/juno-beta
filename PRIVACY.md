# Privacy

This page describes the data handling of **Juno Beta 0.3 (Final)**, version `1.0.0-rc.18`. It is a plain description of the Beta implementation, not a legal privacy policy and not a substitute for your AI provider's terms.

Juno is local-first, but it is not offline. It makes network requests when you use a provider, a browser tool, research, or the update check.

## What stays on your computer

Juno stores its own data in two local folders:

```text
%APPDATA%\Juno        desktop state, window state, logs, crash records, encrypted credentials
%USERPROFILE%\.juno   bots, conversations, memory, routines, artifacts and generated files
```

These folders can contain private conversations, prompts, results and file paths. Treat them as private data.

The local server listens on loopback only. Beta 0.3 does not expose a public inbound port by default. Remote phone, Tailscale and mobile companion flows are deferred for this Beta.

## What leaves your computer

Juno sends data only through the paths below.

### AI providers

When you connect a provider and send a message, the prompt and the context needed for that turn are sent to the provider you selected. That can include conversation history, selected files or excerpts, tool results and system instructions. The provider handles that data under its own terms, retention policy and billing.

Juno does not proxy provider traffic through an owner-operated service. The request goes from your machine to the provider you configured.

### Tools and network access

If you authorize browser, research, computer or terminal tools, those tools can make network requests and read or write files according to the permissions you granted. A research run may fetch public pages and record citations. A browser task may visit sites you ask it to visit. Those requests go to the destinations involved, not to the Juno owner.

### Update metadata

Juno requests a small public JSON file over HTTPS after launch and every six hours:

```text
https://tanishkfr.github.io/juno-update-feed/latest.juno.json
```

The request asks for release metadata only. It does not send your conversations, account identifiers or a Juno account identifier. The hosting provider (GitHub Pages) can see standard request information such as your IP address and user agent. The response is public, signed metadata, not user data.

### Crash records and diagnostics

Juno keeps local crash and error records under `%APPDATA%\Juno\diagnostics`. Nothing is uploaded automatically. On the next launch Juno may offer to report a crash; the offer opens the same reviewed report form described below.

Diagnostics are optional. When you turn them on for a report, Juno includes allowlisted technical fields such as the Juno version, Windows version, architecture and recent in-session error events. It does not include prompts, model responses, files, screenshots, account details or credentials.

### Bug reports and feedback

Juno has no reporting backend and no background upload. **Settings > Help & feedback** prepares a Markdown report locally. If you choose **Open Email Draft**, Juno asks Windows to open a new email in your own mail app, addressed to `madebytanishk@gmail.com`, with the reviewed report in the body.

- Nothing is sent until you press Send in your mail app.
- Your mail provider handles the message under its terms.
- Juno cannot confirm that the email arrived.
- If the report is too long for a mail link, the draft is shortened and says so. Copy Report and Save Report keep the complete text.
- If you choose Copy or Save instead, nothing leaves your computer.

## Credentials

Provider keys are stored in Juno's desktop data folder using the operating system's encrypted credential store (`credentials.bin` under `%APPDATA%\Juno`). The app reports whether a credential is configured but does not display the value back in the interface.

A copied Juno profile is only usable by the same Windows user and machine credential context. Do not share your profile folder, and do not paste keys into a report or an issue.

## What Juno does not collect

Beta 0.3 has no product telemetry, no analytics endpoint, no advertising identifier and no automatic crash upload. It does not create a Juno account or require a cloud sign-in.

This does not cover data collected by the providers and websites you choose to use.

## Retention and deletion

- Local Juno data stays until you delete it.
- Uninstalling Juno removes the application, shortcuts and Windows registration, but keeps `%APPDATA%\Juno` and `%USERPROFILE%\.juno` by default.
- To remove all local Juno data, close Juno, back up anything you need, then delete both folders. Deletion is permanent.
- Sent emails live in your mail account and are governed by that provider.
- The owner keeps reports that testers send by email for triage and release work.

## Third parties

- AI providers, model vendors and any websites you visit are third parties with their own terms.
- GitHub hosts this private repository and the public update metadata.
- Microsoft PowerPoint and FFmpeg are optional local tools, not bundled services.
- Third-party notices and licenses are in [LICENSES.md](LICENSES.md) and [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

## Questions

Use the private feedback route in [FEEDBACK.md](FEEDBACK.md) for questions about this Beta's data handling. Do not include secrets or private documents in a report.
