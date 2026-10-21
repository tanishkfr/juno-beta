# Licensing

This project is open source under the [Apache License 2.0](LICENSE).

## Origin

This codebase began as the open-source edition of **OpenMausBot**
(<https://github.com/milind-soni/OpenMausBot>), Copyright 2026 Milind Soni and
OpenMausBot contributors, and remains a derivative work of it. That project's main
tree was Apache 2.0; a separately licensed `enterprise/` directory sat beside it
under its own terms and is **not** present here — it was removed, and none of its
implementation was copied, ported or recreated. What remains is Apache 2.0
throughout.

Apache 2.0 §4 is satisfied as follows.

- **§4(a)** the License: [`LICENSE`](LICENSE), unchanged, and shipped inside the
  packaged application as `licenses/PRODUCT-LICENSE.txt`.
- **§4(b)** any NOTICE: [`NOTICE`](NOTICE), unchanged, shipped as
  `licenses/PRODUCT-NOTICE.txt`.
- **§4(c)** a statement of changes: the commit history, and
  [`docs/upstream.md`](docs/upstream.md) plus
  [`docs/architecture.md`](docs/architecture.md) for a summary.
- **§4(d)** retained notices: the copyright line in `NOTICE`, the attribution
  comments in `server/contracts.ts` and `src/components/ProviderIcons.tsx`, and
  the [`third_party/`](third_party/) tree are all intact.

Removing visible product identity did not remove required attribution. The
Apache 2.0 license, the NOTICE file, the third-party license texts, the
in-code attribution comments and the upstream credit in this file are legally
required and are kept deliberately; see [`docs/upstream.md`](docs/upstream.md) §2
for the item-by-item list.

The upstream name and mascot are trademarks of Milind Soni. Apache 2.0 grants no
trademark rights (section 6), so this product does not claim them and does not
present itself as OpenMausBot, Maus, SupaMaus or OMB.

## The edition seam

`server/enterprise.ts` remains as a neutral hook point. With no layer to load it
always resolves to the open-source edition:

```
GET /api/edition
→ {"edition":"oss","features":[]}
```

and, if `OMB_LICENSE_KEY` is set, adds a notice saying the key matches no layer.
Every entitlement id is therefore permanently `false`, and every
entitlement-gated surface — white-label brand, OIDC sign-in, the fleet screen,
workspace spend caps, sell prices — is simply absent. Nothing degrades, nothing
errors, and nothing is faked.

A deployment explicitly configured for hosted sign-in (`OMB_ADMIN_URL`,
`OMB_ADMIN_WORKSPACE`, `OMB_ADMIN_MEMBERSHIP`) **fails closed**: it refuses hosted
access rather than falling back to local email or QR credentials. That decision
is made from the environment alone and needs no layer, which is what makes it a
security property rather than a feature. See
[`docs/verification/enterprise-license.md`](docs/verification/enterprise-license.md).

`server/hosted-contract.ts`, `SessionRegistry.issuePortal()` and `server/fleet*.ts`
remain in the tree as part of the OSS seam contract, permanently unreachable from
a license key. They were kept rather than deleted so a future adapter would not
have to be re-derived; see [`docs/upstream.md`](docs/upstream.md) §3.

## Contributions

Contributions are accepted under Apache 2.0. No DCO sign-off is required. Submit
only code you wrote or have the right to contribute. The licensing seam, the
cloud seam and this file are covered by
[`.github/CODEOWNERS`](.github/CODEOWNERS).

## Third-party components and trademarks

Bundled third-party software keeps its own licenses; notices, license texts,
source locations and the SBOM are listed in [NOTICE](NOTICE) and
[`third_party/`](third_party/).
