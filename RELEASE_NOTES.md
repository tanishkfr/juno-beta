# Juno v0.5 Beta — Release Notes

**Public Beta · Windows 11 x64 · Version `0.5.0-rc.1` · Unsigned installer · Manual updates**

Release date: 2026-11-15

| Field | Value |
|---|---|
| Public title | Juno v0.5 Beta |
| Installed version | `0.5.0-rc.1` (Settings shows “Juno v0.5 Beta · 0.5.0-rc.1”) |
| Installer | `juno-0.5.0-rc.1-setup.exe` |
| Size | 261,843,896 bytes (249.7 MiB) |
| SHA-256 | `B8C931EC42D7892B5FA8E64781220A3A270895AD586636801E53C1452CEBB5C6` |
| Source revision | `9a53d136` |
| Platform | Windows 11 x64 |
| Signature | **NotSigned** |

> This is a release candidate for the public beta, not a stable `0.5.0` binary.
> If you are looking for an older build, every published release remains on the
> [releases page](https://github.com/tanishkfr/juno-beta/releases).

## Highlights

### One unified, companion-first workspace

The separate Bot and Code modes are gone. A single workspace carries the
companion sidebar, the conversation, Code and Mission work, with one composer and
one history. Code work stays attached to the conversation that authorized it.

### Refined sidebar, composer and atmosphere

- Recent Work sits directly below the companions, grouped by project, with
  compact status marks and clear selected states.
- The composer is a single compact surface: attachments and secondary tools in
  the toolbar, **Code** and **Mission** as first-class actions, a clean multiline
  input, and the same keyboard and model controls as before.
- A Juno-inspired pixel atmosphere fills a genuinely empty conversation and
  settles into a neutral canvas on the first message. Existing threads open in
  the settled state, and reduced-motion preferences are respected.
- Both the OLED-black and warm light themes were refined, with contrast checked
  across surfaces. Replies and your own messages carry the reading weight; tool
  activity stays quiet.

### Missions with preview and durable recovery

A Mission is previewed with its objective, expected effects, model route and
authorization boundary before anything runs. After you authorize it, Juno hands
the work to Code without asking you to repeat the request. A pending decision,
the exact child identity and its attempt survive a restart; an uncertain side
effect is never replayed and a second child is never created.

### Read-only Code answers

A Code question that asks for an explanation — or that says no file may change —
is a normal, verifiable request. Juno evaluates the run's own before/after
fingerprints: nothing changed is a pass, and a worker that writes during a
read-only run fails validation and is never offered for transfer. A read-only run
never claims Ariadne verification.

### Ariadne verification

Ariadne locally verifies owner-declared checks and the Code revision it is given.
Juno shows “the model said so” and “independently verified” as different things.
Ariadne does not prove every model statement or external side effect.

### Provider and model fixes

- ChatGPT-plan catalogues are read from the connected account and report a retry
  state instead of a blank list.
- An explicit model choice is never silently replaced; a retired model is
  reported and you are asked to choose another.
- A rejected credential found while reading a catalogue is reported as an
  authentication problem, not a catalogue outage.

### Update announcements

A signed manifest can announce a newer release and name its own HTTPS download
page. The page is validated before it is opened, invalid signatures and unsafe
URLs are refused, and **nothing is downloaded or installed automatically**.

## Download and verify

Download `juno-0.5.0-rc.1-setup.exe` and `SHA256SUMS.txt` from the release page:

<https://github.com/tanishkfr/juno-beta/releases/tag/v0.5.0-rc.1>

```powershell
Get-FileHash .\juno-0.5.0-rc.1-setup.exe -Algorithm SHA256
```

Expected:

```text
B8C931EC42D7892B5FA8E64781220A3A270895AD586636801E53C1452CEBB5C6  juno-0.5.0-rc.1-setup.exe
```

The installer is **unsigned**. Windows may show Unknown Publisher or SmartScreen.
Verify the checksum, and do not disable Windows security controls. Full steps:
[INSTALL.md](INSTALL.md).

## Upgrading from v0.4.x

1. Back up your workspace first (Settings → Backups → Export full backup, or a
   copy of `%USERPROFILE%\.juno`).
2. Quit Juno completely.
3. Run the v0.5 installer. It upgrades in place and preserves companions,
   conversations, credentials, settings and work items.
4. Open Juno and confirm your provider connections and model pins.

An in-place downgrade is **not supported**. Restore a pre-upgrade backup into a
fresh profile if you need to return to an earlier build.

## Known issues

The complete, current list — including the one open issue and the accepted beta
limitations — is in [KNOWN_ISSUES.md](KNOWN_ISSUES.md), and the same records are
published as structured data at
[`support/v0.5.0-rc.1/known-issues.json`](support/v0.5.0-rc.1/known-issues.json).

Highlights:

- The installer is unsigned and updates are manual.
- Code execution needs the external OMP runtime, which is not bundled.
- External providers require your own account, access and quota.
- There is no workspace-wide spending hard cap.
- A carried-over conversation can fail to load on an upgraded profile (see the
  known-issues list for details).

## Not claimed

- No Authenticode publisher trust and no SmartScreen reputation.
- No automatic installer download or installation.
- No guarantee that an external provider keeps offering a given model.
- No general remote/paired-device mutation support.
- No workspace-wide spending guarantee.
