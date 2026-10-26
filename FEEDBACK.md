# Feedback and bug reports

Juno Beta 0.3 is small and private. Specific, reproducible reports are more useful than a score.

## Primary route: from inside Juno

1. Open **Settings > Help & feedback**.
2. Choose **Report a bug** or **Share feedback**.
3. Describe what happened. Add steps, expected behavior and actual behavior where you can.
4. Turn on **Include technical diagnostics** only if you are comfortable sharing the allowlisted technical fields it lists.
5. Review the report preview. It is the exact text that will be used.
6. Choose **Open Email Draft**.

Juno opens a new email in your own mail app, addressed to:

```text
madebytanishk@gmail.com
```

Review the message and press **Send** yourself. Juno does not send it, has no reporting server and cannot confirm that it arrived.

### What the draft contains

- A stable report ID, for example `JUNO-20261026-A1B2C3D4`.
- The Juno version, report kind and timestamp.
- Your description, and the optional sections you filled in.
- Diagnostics only if you turned them on.
- A privacy note describing what was included.

### Long reports

A mail link has a practical length limit. If your report is longer, Juno opens a **shortened draft** and tells you exactly how many characters fit, for example "1105 of 6177 characters". The complete report is still available through **Copy Report** or **Save Report**; paste or attach it in the email before sending.

Do not assume the shortened draft contains everything. Read the notice.

### If the email app does not open

Windows may ask which app should open the `mailto` link. Choose your mail app. If no mail app is configured, Juno says so and leaves Copy and Save available. Copy the report and send it to `madebytanishk@gmail.com` from any mail account.

### Copy and Save

**Copy Report** puts the complete Markdown report on the clipboard. **Save Report** writes it to a file you choose. Neither action uploads anything.

## Crash reports

When Juno records an unexpected error, it keeps a local crash record. On the next launch it may offer to report the problem.

- The offer opens the same reviewed form, with the crash classification attached.
- Nothing is sent automatically, and the mail app is not opened automatically.
- Diagnostics are still optional.
- The local record stays on your PC until you clear it in **Settings > Help & feedback > Crash reports** (or delete the Juno data folder).

## Alternative route: GitHub Issues

If you have access to this private repository, you can open an issue:

<https://github.com/tanishkfr/juno-beta/issues/new/choose>

You must be an invited read collaborator. Do not post logs, keys or private documents in a public place, and do not copy the private repository contents elsewhere.

## What makes a useful report

1. **Juno version.** Settings > General shows the version, for example `Juno Beta 0.3 · 1.0.0-rc.18`.
2. **Windows version.** For example Windows 11 24H2, build 26200, x64.
3. **Feature.** Agent, Code, Library, Research, voice, Settings, onboarding or installer.
4. **Expected behavior.** What you thought would happen.
5. **Actual behavior.** What happened, including the exact message or status text.
6. **Steps to reproduce.** The smallest sequence that shows the problem.
7. **Repeatability.** Every time, sometimes or once.
8. **Evidence.** A screenshot or a short log excerpt only if it is safe to share.

## Product bugs versus provider problems

Some failures come from the provider account, not from Juno.

Check the provider first if you see:

- authentication, expired key or permission errors;
- quota, rate-limit or billing errors;
- a provider status page reporting an outage;
- the same failure in the provider's own dashboard or another client.

Include the Juno error code and provider name if you still report it. Never include the API key. Re-enter a revoked key in **Settings > Providers**; Juno cannot display the stored value.

## Privacy and redaction

Before sending or attaching anything, remove:

- API keys, access tokens, OAuth codes and cookies;
- email addresses and account identifiers you do not want to share;
- private file paths, document names and screenshots of personal content;
- raw logs unless you have reviewed them.

Juno does not upload logs automatically. A log can still contain local paths, prompts or result snippets, so review it first.

## Response expectations

Reports are triaged by severity:

- crash, data loss or an authorization problem: highest priority;
- broken Agent or Code core path: next candidate;
- visual or copy issue: batched into a later Beta pass.

This is a private Beta with no guaranteed response time or support SLA. The owner may ask for a reproduction in a disposable project. Do not test destructive actions on work you cannot lose.
