# Release asset policy (proposal)

This policy is prepared for owner approval. It does not publish or modify an existing
release by itself.

## Required assets for a methodology release

| Asset | Purpose |
|---|---|
| `GALDUR-Methodology-vX.Y-CS.pdf` | Versioned Czech reading/printing edition |
| `GALDUR-Methodology-vX.Y-EN.pdf` | Versioned English reading/printing edition |
| `galdur-templates-vX.Y.zip` | Only reusable `templates/` payloads plus `LICENSE` |
| `galdur-web-vX.Y.zip` | Self-contained HTML documentation, public assets, both licenses |
| `SHA256SUMS` | SHA-256 digest of every release asset except signature material |
| `SHA256SUMS.sig` and signer certificate/bundle | Verifiable signature and provenance for `SHA256SUMS` |

The release notes must name the exact source commit and explain the license boundary.
PDFs are documentation under CC BY 4.0. The templates archive is MIT; it must not imply
that the methodology text or trademarks are MIT-licensed.

## Reproducible preparation

1. Build all assets from a clean checkout of the release tag.
2. Use deterministic archive ordering and timestamps where the tooling permits it.
3. Inspect archive manifests; reject absolute paths, parent traversal, secrets, internal
   hosts, customer data, and untracked files.
4. Render-smoke both PDFs and both HTML language surfaces.
5. Generate checksums only after the files are final:

   ```sh
   sha256sum GALDUR-Methodology-vX.Y-CS.pdf \
     GALDUR-Methodology-vX.Y-EN.pdf \
     galdur-templates-vX.Y.zip galdur-web-vX.Y.zip > SHA256SUMS
   sha256sum --check SHA256SUMS
   ```

6. Sign `SHA256SUMS`, not each asset independently. Preferred path: keyless Sigstore
   `cosign sign-blob` from a protected release workflow, retaining its certificate and
   transparency-log bundle. If an offline signing key is chosen instead, document key
   custody, publish its fingerprint through an independent trusted channel, and test
   verification before release.
7. Create a **draft** release first. A second person verifies filenames, sizes,
   checksums, signature, source tag/commit, CS/EN versions, and licenses.
8. Publish only with the explicit owner approval receipt required by the guarded release
   tool.

## v0.95 backfill

Do not silently attach newly generated files as if they were the original 2026-09-07
artifacts. Build them from tag `v0.95`, record the build date and source commit
`38020c34024000a7810eccd66d03fbe27e669c42`, and state clearly in the release notes that
the assets were backfilled after the original release. If the current PDF source cannot
be reproduced exactly from that tag, publish a new patch release instead.
