# Feedback

Juno Beta 0.1 is small and private. Direct, specific reports are more useful than a score.

## Where

Open an issue in this repository:

- **Bug report:** <https://github.com/tanishkfr/juno-beta/issues/new?template=bug_report.yml>
- **Feature request:** <https://github.com/tanishkfr/juno-beta/issues/new?template=feature_request.yml>

You need to be an invited read collaborator to open an issue. If you cannot access the repository,
ask the owner for an invitation; do not post logs or keys elsewhere.

## A useful bug report

Please include:

1. **Juno version** — Settings → General shows `Juno Beta 0.1 · 1.0.0-rc.7`; the installer file is
   `juno-1.0.0-rc.7-setup.exe`.
2. **Windows version** — e.g. Windows 11 Home 10.0.26200, x64.
3. **Feature** — Agent, Code, Results, Voice, Settings, onboarding, installer, etc.
4. **Expected behavior** — what you thought would happen.
5. **Actual behavior** — what happened, including the exact message if there is one.
6. **Steps to reproduce** — the smallest sequence that shows it.
7. **Repeats?** — every time, sometimes, or once.
8. **Screenshot/log** — only if safe. Remove API keys, access tokens, cookies, email addresses,
   private file paths and personal documents.

## Privacy warning

Do **not** attach a raw `server.log` without reviewing it. Juno does not upload logs automatically,
but logs can contain local paths, provider names, prompts or result snippets. Redact before sharing.
Never paste an API key, OAuth token, session cookie or private document into an issue.

## What happens next

Reports are triaged by severity:

- crash / data loss / authorization bypass — immediate;
- broken core Agent or Code path — next candidate;
- visual or copy issue — batched into the next Beta polish pass.

This is a private Beta; there is no guaranteed response time or support SLA. The owner may ask for a
reproduction in a disposable project. Do not test destructive actions on work you cannot lose.
