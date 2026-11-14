# Reference

Details the README points at. Inputs and the usage example stay in the README. Defaults are the `default:` lines in `action.yml`.

## Pin

| What | Value |
|------|--------|
| This action | Pin a commit SHA. The default branch moves. Do not use `@main` as the primary example. |
| HelixTest binaries | GitHub Release `v0.1.3` (`helixtest-*` plus `.sha256`). `action.yml` sets `version` default to `v0.1.3`. |
| Schema source of truth | Published GA4GH OpenAPI, vendored in HelixTest. The Ferrum [utoipa dump](https://github.com/SynapticFour/Ferrum/blob/main/docs/openapi/ferrum.openapi.json) is an implementation map only. |
| Default `--mode` | `ferrum` |

The published HelixTest tag `v0.1.3` peels to `1832c043e1679ec283cb2113510ee33684317cce`. HelixTest's default branch is later than that tag. This action downloads the release assets for the `version` input. It does not build HelixTest's default branch.

## Modes

| Mode | What it runs | What it is not |
|------|----------------|----------------|
| `ferrum` | HelixTest against a running Ferrum, or a compatible HTTP surface | Not authentication unless your stack turned it on. Not certification. |
| `ferrum+infra` | The same, plus ga4gh-infra (broker, registry, Passport-on-DRS). The stack must already be up. | Not this action starting Compose. |
| GHCR auth-on | HS256 JWT on published `ferrum:edge` | Not this action. That job lives in HelixTest (`.github/workflows/live-ferrum-ghcr-auth.yml`). |

`ferrum+infra` after you started Ferrum `make up-pilot-local`, or the equivalent:

```yaml
- uses: SynapticFour/helixtest-action@SHA
  with:
    version: v0.1.3
    mode: ferrum+infra
    profile: ferrum-infra-pilot
  env:
    GATEWAY_BASE: http://127.0.0.1:8080
```

Replace `SHA` with the commit you have read.

## Runners

Release assets exist for linux-gnu x86_64, linux-gnu aarch64, and darwin aarch64. `action.yml` maps `Linux-x86_64`, `Linux-aarch64`, `Linux-arm64`, and `Darwin-arm64` to those assets. Any other runner fails and prints that list. There is no Windows binary.

## What this is not

- Not a Ferrum installer
- Not a combined product
- Not Passport issuance
- Not HELIOS pipeline evidence

CLI install notes: [HelixTest INSTALL](https://github.com/SynapticFour/HelixTest/blob/main/docs/INSTALL.md).
