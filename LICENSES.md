# Licenses

Juno Beta 0.1 is distributed under the **Apache License 2.0**. The full text is in
[LICENSE](LICENSE), and the preserved upstream attribution is in [NOTICE](NOTICE).

## Provenance

Juno is a derivative work of the earlier Apache-2.0 **OpenMausBot** project, Copyright 2026
Milind Soni and OpenMausBot contributors. The upstream license and NOTICE are preserved. The
product does not claim the upstream name, mascot or trademarks. See [LICENSING.md](LICENSING.md).

## Third-party components

The packaged application includes third-party software with its own terms. Full notices are in
[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md); the installer also carries license texts under
`Resources/licenses/`.

| Component | License | Notes |
|---|---|---|
| Electron / Chromium | MIT / BSD-style | Desktop runtime; Chromium notices ship with the app |
| node-pty and bundled ConPTY | MIT | Terminal runtime |
| cloudflared | Apache-2.0 | Optional private tunnel binary |
| agent-browser / Chromium headless | Apache-2.0 | Managed browser engine |
| CUA driver | MIT | Computer-use driver; third-party notices included |
| `@hpke/core`, `@hpke/common` | MIT | Pairing crypto |
| models.dev catalog / OpenCode refresh logic | MIT | Model metadata |
| sharp 0.35.3 | Apache-2.0 | Image rendering |
| `@img/sharp-win32-x64` (libvips) | Apache-2.0; libvips LGPL-2.1-or-later | Native image runtime |
| detect-libc | Apache-2.0 | sharp dependency |
| semver | ISC | sharp dependency |
| `@img/colour` | Apache-2.0 | sharp dependency |
| Boreal coordinator | Apache-2.0 | Frozen reviewed engine; Python/PyInstaller/native notices under `Resources/boreal/runtime-licences/` |

## Redistribution

Do not redistribute the private installer or this repository. The private Beta access is granted to
named testers only. If you need to evaluate the source, use the private source repository under the
terms granted by its owner.

No third-party software was added to hide a missing dependency. Optional tools such as Microsoft
PowerPoint and FFmpeg are not bundled; their own licenses apply if you install them.
