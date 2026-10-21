# Release asset policy

Scope approved by the owner (2026-09-21; signature deferral for the v0.95 backfill
approved 2026-10-21). This policy does not publish or modify an existing release by itself.

## Required assets for a methodology release

| Asset | Purpose |
|---|---|
| `galdur-templates-vX.Y.zip` | Only reusable `templates/` payloads plus `LICENSE` |
| `SHA256SUMS` | SHA-256 digest of the templates archive |
| `SHA256SUMS.sig` and signer certificate/bundle | Verifiable signature and provenance for `SHA256SUMS` (deferred for the v0.95 backfill, see below) |

The release notes must name the exact source commit and explain the license boundary.
The templates archive is MIT; it must not imply that the methodology text or trademarks
are MIT-licensed.

**Methodology PDFs and an HTML/web archive are intentionally not release assets.** The
methodology text remains free to read online in Czech and English, while the printable
PDF is delivered through the paid 5/10 EUR Stripe flow. Attaching PDFs or a web bundle
to GitHub would bypass that distribution model. Only the MIT templates are offered as
freely downloadable release assets.

## Reproducible preparation

1. Build the templates archive from a clean checkout of the release tag.
2. Use deterministic archive ordering and timestamps where the tooling permits it.
3. Inspect archive manifests; reject absolute paths, parent traversal, secrets, internal
   hosts, customer data, and untracked files.
4. Verify that the archive contains only `templates/` and `LICENSE`, with no symlinks,
   generated caches, or unrelated repository files.
5. Generate checksums only after the files are final:

   ```sh
   sha256sum galdur-templates-vX.Y.zip > SHA256SUMS
   sha256sum --check SHA256SUMS
   ```

6. Sign `SHA256SUMS`, not each asset independently. Preferred path: keyless Sigstore
   `cosign sign-blob` from a protected release workflow, retaining its certificate and
   transparency-log bundle. If an offline signing key is chosen instead, document key
   custody, publish its fingerprint through an independent trusted channel, and test
   verification before release.
7. Create a **draft** release first. A second person verifies filenames, sizes,
   archive manifest, checksum, signature, source tag/commit, and MIT license inclusion.
8. Publish only with the explicit owner approval receipt required by the guarded release
   tool.

## v0.95 backfill

Do not silently attach newly generated files as if they were the original 2026-09-07
artifacts. Build them from tag `v0.95`, record the build date and source commit
`38020c34024000a7810eccd66d03fbe27e669c42`, and state clearly in the release notes that
the assets were backfilled after the original release. If the templates archive cannot
be reproduced cleanly from that tag, publish a new patch release instead.

### v0.95 backfill without a signature

The v0.95 templates archive is published with `SHA256SUMS` but without `SHA256SUMS.sig`.
Signing will be added once the release-signing setup is in place; until then the checksum
only protects against a corrupted download, not against a compromised release page.

Anyone can check the archive against the public tag instead: every file in
`galdur-templates-v0.95.zip` is identical to the same path in tag `v0.95`.

```sh
git clone https://github.com/Yggnet-Labs/Galdur-Methodology.git galdur-src
mkdir galdur-tag galdur-zip
git -C galdur-src archive v0.95 LICENSE templates | tar -x -C galdur-tag
unzip -q galdur-templates-v0.95.zip -d galdur-zip
diff -r galdur-tag galdur-zip && echo "identical to tag v0.95"
```

