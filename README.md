# Juno Beta 0.1 — Private Tester Distribution

This repository is the private download and feedback channel for **Juno Beta 0.1**, a Windows
desktop workspace for a personal AI agent and coding work.

Juno is a local-first Electron application. It combines:

- a persistent Agent with conversations, tool calls, approvals, memory, routines and artifacts;
- a Code workspace with project attachment, Code/Ask/Orchestrate modes, exact model selection,
  staged review, apply/discard and a terminal;
- a Results shelf for generated presentations, PDFs and short procedural videos;
- local Windows speech output.

## Status

This is a **limited private Beta**, not a general release. It is intentionally narrow:

- Windows 11 x64 only.
- The installer is **unsigned**. SmartScreen may warn on first run; see [INSTALL.md](INSTALL.md).
- Installation evidence comes from the owner's development PC, not an independent clean Windows
  machine. External testers are providing the additional machine evidence.
- Automatic repair, parallel mutating Code workers, AI-generated video and remote/cloud/mobile
  workflows are not qualified for this Beta.
- Human microphone dictation and voice barge-in are not qualified.
- The 30-task frozen benchmark has not been executed.

Read [KNOWN_ISSUES.md](KNOWN_ISSUES.md) before installing, and [PRIVACY.md](PRIVACY.md) for how
local data and provider traffic are handled.

## Download and install

1. Ask the owner to invite your GitHub account as a **read** collaborator on this private
   repository. A copied release URL alone will not grant access.
2. Open the latest prerelease:
   <https://github.com/tanishkfr/juno-beta/releases/latest>
3. Download `juno-1.0.0-rc.7-setup.exe` and, if you wish, verify it with `SHA256SUMS.txt`.
4. Follow [INSTALL.md](INSTALL.md).

The current installer is **Juno Beta 0.1**, internally `1.0.0-rc.7`.

## First run

- Choose your name and a starting assistant.
- Connect a provider you have an account for. The Beta was qualified with Command Code; other
  routes may be visible but are not all equally qualified.
- Try the Agent with a small question, or open **Code** and attach a disposable project.
- Generated results appear in **Results**. A deck may need PowerPoint installed for slide previews
  and PDF export; a video may need FFmpeg.
- Quit from the tray if you want the background host to stop. Closing the window keeps agents
  running when the host setting is on.

## Feedback

Use the issue templates:

- [Report a bug](https://github.com/tanishkfr/juno-beta/issues/new/choose)
- [Request a feature](https://github.com/tanishkfr/juno-beta/issues/new/choose)

See [FEEDBACK.md](FEEDBACK.md) for the exact details that make a report useful. Never paste API
keys, tokens, session cookies or private documents.

## Access policy

The repository is private. Testers are invited as collaborators with read access to releases and
issues. Do not redistribute the installer or repository access. Access can be removed at any time.

## Licensing

Juno is Apache-2.0 licensed. The installer and this repository include the product license, the
upstream NOTICE, and third-party notices. See [LICENSES.md](LICENSES.md).
