# IrnBru gh Isotope

This branch supplies gh to IrnBru. It preserves GitHub CLI history and licenses
and the existing Automic Vault integration; no Automic Vault repository or
release is transferred or changed.

## Source provenance

- Upstream: cli/cli v2.103.3,
  63837fb778d6a39f02be0ce76ff89f2bc8d74bdc.
- Inherited integration: automic-vault/gh-cli,
  222f7840e0aae5c6d7945525cd26fb1aa8b6ec27.
- The inherited v2.103.3 tag names that patched AV commit, not the upstream one.
  IrnBru releases use distinct names, starting with v2.103.3-irnbru.1.
- The irnbru branch commits the existing AV5 adaptation. It retains the
  com.automicvault.av5.approval endpoint and authenticates the exact helper
  signing identity. These identifiers are compatibility boundaries.

## Patch inventory

The inherited delta covers credential custody and refreshable tokens
(internal/keyring, internal/config), explicit provider-error propagation
(api, auth commands, factory), request command/working-directory context and
approval notifications, custom Vault Git remote recognition (git, ghrepo,
internal/gh), version branding, related tests, and fork documentation/CI.

Inspect the complete delta against the upstream SHA, not the inherited tag.
Custom remote handling, branding and inherited automation need separate review
before the first IrnBru release; this source bootstrap preserves working behavior.

Keep patches minimal. Installation grants no credential authority. Signing
establishes identity, not trustworthiness. A credential-consuming Target controls
the credential after receipt.

## Validation and release

Use the Go toolchain in go.mod. Run go test ./internal/keyring, the macOS
script/test-vault-keyring.py transport tests, go test ./..., and make lint.
Live acceptance tests require separately authorized disposable resources.

Inherited Actions stay disabled until reviewed. Do not add signing credentials
to pull-request workflows. No IrnBru binary release exists yet. Release metadata
must record both source commits, upstream version and Isotope revision,
toolchains, architecture, minimum OS, protocol compatibility, final signed
artifact digest/size and expected signing identity. Never replace released bytes.

Shared security terms and limits:
- https://github.com/automic-vault/automic-vault/blob/main/docs/domain-language.md
- https://github.com/automic-vault/automic-vault/blob/main/docs/architecture.md
- https://github.com/automic-vault/automic-vault/blob/main/docs/positioning.md

Bootstrap validation (November 11, 2026): go fix ./internal/keyring made no
additional changes; focused keyring tests, the macOS XPC request-builder test
and go test ./... passed. make lint reports four inherited unused functions
in internal/config/refreshable.go (refreshableFromConfig, optionalSeconds,
optionalTimestamp and isKeyNotFound). That file is unchanged from the AV source
pin. Resolve these in a separately reviewed maintenance change before release.
