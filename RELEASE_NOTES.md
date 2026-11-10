# Juno v0.4.1 Beta — Unified Agent Runtime

**Public Beta · Windows 11 x64 · Version 0.4.1 · Unsigned installer · Manual updates**

Juno v0.4.1 brings Juno's execution experiences onto one shared task system. The
product behaviour, provider routes, Code workspace boundary and Ariadne's
independent verification are preserved. This is not a frontend rewrite, and it
does not replace Boreal, Pi or OMP.

## Download

| Variant | File | Size |
|---|---|---:|
| **Compact (recommended)** | `juno-0.4.1-setup.exe` | 271,664,867 B |
| **Full/offline** | `juno-0.4.1-full-setup.exe` | 488,550,122 B |

The full variant includes the pinned browser engine and Whisper base.en model.
External model providers still need internet access, an account and quota.

## Verify before installing

```powershell
Get-FileHash .\juno-0.4.1-setup.exe -Algorithm SHA256
Get-FileHash .\juno-0.4.1-full-setup.exe -Algorithm SHA256
```

Expected:

```text
3B6B3EF3EC870CA779E1A7B623A3D970D468729F0B9BF2608B171F2400233EBD  juno-0.4.1-setup.exe
C64A3441209BECB10A569498C8FDF403C41592EE5779880B98B8576BAA8CD864  juno-0.4.1-full-setup.exe
```

The installer is **unsigned**. Windows may show Unknown Publisher or
SmartScreen. Continue only if the checksum matches. Do not disable Windows
security controls. Some managed PCs may block the installer; stop and ask your
administrator if that happens.

## Main improvement: one shared task system

Juno now uses a shared task system across its different execution experiences.
Bot Mode, Code Mode, Council, `/btw`, room/team conversations and delegated work
record their task through the same Juno runtime.

This brings more consistent task tracking, cancellation, recovery, model-call
accounting and permission handling. A task keeps one identity from admission to
its terminal record, and it settles once even if a provider event is repeated or
a crash interrupts the flow.

## Specific improvements

- **Shared task identity and lifecycle across Bot Mode and Code Mode.** Every
  direct Bot turn and Code run is admitted through the same runtime, with the
  execution profile, parent relationship and authority snapshot recorded on the
  task.
- **Council planner/reviewer call tracking.** Planner and reviewer calls are
  durable task calls with their own model, usage and terminal state. The parent
  stays in verification until the mandatory reviewer settles. A late usage
  report is booked as late usage without rewriting the terminal receipt.
- **`/btw` side-task identity and isolation.** The side task gets its own
  profile, runtime parent, transcript, budget and cancellation. The main task's
  usage does not absorb the side conversation.
- **Room/team conversations participate in the same task system.** A room turn
  creates one room profile task. Each member provider call is recorded under it
  with actor, model, usage and terminal status. The room task stays open across
  its handoff tree and settles once, including cancellation and provider
  failure.
- **More reliable cancellation and interrupted-task handling.** Cancellation
  settles through the runtime and cannot be recorded as success. A late provider
  completion cannot reopen a finished task. Restart recovery marks unfinished
  work honestly instead of inventing a reply.
- **Durable usage and terminal records.** Duplicate completion events cannot
  double-complete or double-charge a task. A crash between a usage claim and its
  ledger append is replayed from the stored claim on the next launch.
- **Stronger Code Mode model-selection boundaries.** Before Code work starts,
  Juno qualifies an exact model against the live worker catalogue. It sends an
  explicit worker contract and verifies the model Boreal actually bound. A
  substitution or unreviewed fallback stops the run.
- **Continued Ariadne verification.** Ariadne remains independent. No executor
  can mark its own claims verified; Code review and Council verdicts remain
  advisory evidence only.
- **Crash-notice behavior qualified.** A hard process kill does not fabricate a
  notice or an assistant reply. A recorded renderer error offers the reviewed
  report action once, and dismissal is durable across restarts.
- **Preserved existing app performance.** The Juno-controlled durable task
  overhead is unchanged at roughly 7 ms p50. Warm reply time remains
  provider-bound.
- **Existing compact/full distribution options.** The compact installer remains
  the default. The full/offline variant bundles the optional browser engine and
  Whisper model.

Boreal, Pi and OMP have **not** been removed. They remain bounded execution
components behind the Juno task system. Boreal still coordinates Code execution,
OMP remains the Code worker runtime, and Pi remains a provider/agent executor.

## Performance

Qualified measurements from the final candidate on the same Windows 11 x64
machine and tested provider route:

| Measurement | Result |
|---|---:|
| Warm short reply, end to end | **2.29–2.92 s** |
| Durable task overhead | **7.06 ms p50** |
| Compact installer | **271.7 MB** (271,664,867 B) |
| Full/offline installer | **488.6 MB** (488,550,122 B) |

These are measurements, not guaranteed timings. They are not a comparison
between different providers, and they do not imply that the underlying models
became faster or smarter. Provider latency, network conditions and the selected
model dominate reply time.

## Compatibility and upgrade

- Product identity stays `Juno` / `com.agent.app`; bots, conversations, work
  items, approvals, usage, memory and credentials remain in place.
- Installing over v0.4.0 is an in-place upgrade. Keep the previous installer for
  rollback.
- The task-runtime tables are additive. A v0.4.0 build can still open the
  profile if you roll back; it ignores the new tables and rewrites the
  schema-version metadata. Reinstalling v0.4.1 restores the newer schema.
- Back up `%USERPROFILE%\.juno` and `%APPDATA%\Juno` before upgrading or rolling
  back.
- v0.4.0 remains available at
  <https://github.com/tanishkfr/juno-beta/releases/tag/v0.4.0>.

## Known limitations

- The installer is unsigned. There is no Authenticode publisher identity and no
  SmartScreen reputation.
- Updates are manual. The signed automatic-installer upgrade path is not
  qualified. The authenticated announcement feed reports an available version
  but never downloads or executes an installer.
- External providers need your own account, subscription, network access and
  quota. Subscription-backed usage is often unpriced and remains unknown, not
  zero.
- A workspace-wide hard spending cap remains unenforceable across some external
  provider routes. Boreal internal worker iterations are not all bounded by
  Juno's model-call ceiling.
- Live microphone recording was not exercised during final qualification. The
  installed app reported its speech engine, microphone, Windows recognizers and
  on-device Whisper model ready, and the bundled Whisper engine transcribed a
  synthetic WAV exactly.
- The tested browser model omitted a required `tabId` on its initial close call.
  Juno reported the error honestly, and the session was subsequently released
  with the shipped browser engine.
- A clean-room Windows VM was not used. The real installed full/offline variant
  was tested on the owner's existing Windows environment. Computer-control
  qualification used a packaged read-only runtime probe rather than a full
  model-driven interaction.

See [KNOWN_ISSUES.md](KNOWN_ISSUES.md) for the complete list and
[SECURITY.md](SECURITY.md) for the security note.

## Install and feedback

See [INSTALL.md](INSTALL.md) for installation, upgrade, optional runtime
downloads, hash validation, troubleshooting and rollback.

Use **Settings > Help & feedback > Report a bug** to prepare a reviewed email
draft, or open an issue at
<https://github.com/tanishkfr/juno-beta/issues>. Remove API keys, tokens,
cookies and private file paths before sending.

---

**Juno v0.4.1 Beta — Unified Agent Runtime**  
Released: 2026-11-10
