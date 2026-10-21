# Privacy

Juno is local-first. This page describes what the Beta does; it is not a legal privacy policy or a
substitute for your provider's terms.

## What stays on your computer

- Agents, conversations, memory, routines, artifact files and generated work.
- Desktop settings, window state and logs.
- Provider keys, stored through the operating system credential store and write-only through the
  API.

Data locations:

```text
%APPDATA%\Juno          desktop state, logs, OS-encrypted credentials
~/.juno                 agents, conversations, memory, routines, artifacts
```

## What leaves your computer

- Model traffic to the provider you connect. The prompt and relevant conversation/tool context are
  sent to that provider under its terms.
- Web requests needed by an Agent or a research run, using the browser/search path the task
  selects.
- Nothing else is uploaded by Juno Beta 0.1. There is no product telemetry, analytics endpoint or
  automatic crash upload added for this Beta.

## Credentials

Provider keys are encrypted with the operating system credential store and are not returned to the
renderer. The UI reports whether a credential is configured, not its value. A copied profile is
only readable by the same Windows user; testers should not share their profile directory.

## Diagnostics

The app can export diagnostics on request and keeps local logs. Export is user-initiated; logs and
screenshots may contain local paths, prompts or result text. Review and redact before sharing.
Never post keys, tokens or private documents.

## Deletion

Uninstalling the app removes the application and shortcuts but preserves `%APPDATA%\Juno` and
`~/.juno` by default. Delete those directories yourself if you want to remove all local Juno data.
Back up anything you need first; deletion is not recoverable.

## Third parties

- Provider names, models and terms are the provider's.
- PowerPoint and FFmpeg are optional local tools, not bundled with this Beta.
- Third-party notices and licenses are in [LICENSES.md](LICENSES.md).

Questions about this Beta's data handling can be raised through the private feedback channel.
