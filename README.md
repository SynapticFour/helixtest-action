# helixtest-action

GitHub Action wrapper around the **HelixTest** CLI (`v0.1.2` release binaries). Apache-2.0. **Not a product SKU.** Same ambassador as [HelixTest](https://github.com/SynapticFour/HelixTest).

The action **does not start Ferrum, ga4gh-infra, or BRA.** Point it at a stack you already brought up in the job (or a public URL). Results are **not** official GA4GH certification.

## Pin

| What | Value |
|------|--------|
| HelixTest binaries | GitHub Release **v0.1.2** (`helixtest-*` + `.sha256`) |
| Schema source of truth | Published GA4GH OpenAPI (vendored in HelixTest). Ferrum [utoipa dump](https://github.com/SynapticFour/Ferrum/blob/main/docs/openapi/ferrum.openapi.json) is an implementation map only. |
| Default `--mode` | `ferrum` |

Until this repo has its own tag, pin the action at a commit SHA on `main`.

## Modes (what a buyer can claim)

| Mode | What it proves | What it is not |
|------|----------------|----------------|
| `ferrum` | HelixTest against a running Ferrum (or compatible) HTTP surface | Not auth-on unless your stack is. Not certification. |
| `ferrum+infra` | Same plus ga4gh-infra (broker/registry/Passport-on-DRS). Stack must already be up. | Not this Action starting compose. Hosted Synaptic Four proof is Ferrum workflow `helixtest-ferrum-infra.yml`. |
| GHCR **auth-on** | HS256 JWT on published `ferrum:v0.3.1-edge` | **Not this Action.** That job lives in HelixTest (`live-ferrum-ghcr-auth.yml`). Demo Live GHCR stays auth-off. |

## Usage

```yaml
- uses: SynapticFour/helixtest-action@main   # pin a SHA in production
  with:
    version: v0.1.2
    mode: ferrum
    only: beacon          # empty = --all
    fail-level: "2"
    # run: "false"   # install-only (used by this repo's CI)
  env:
    GATEWAY_BASE: http://127.0.0.1:8080
    BEACON_URL: http://127.0.0.1:8080/ga4gh/beacon/v2
    DRS_URL: http://127.0.0.1:8080/ga4gh/drs/v1
```

`ferrum+infra` example (after you started Ferrum `make up-pilot-local` or equivalent):

```yaml
- uses: SynapticFour/helixtest-action@main
  with:
    version: v0.1.2
    mode: ferrum+infra
    profile: ferrum-infra-pilot
  env:
    GATEWAY_BASE: http://127.0.0.1:8080
```

## Runners

Release assets exist for **linux-gnu x86_64**, **linux-gnu aarch64**, **darwin aarch64**. Other runners fail with that list — there is no Windows binary.

## What this is not

- Not a Ferrum installer
- Not a combo SKU
- Not Passport issuance
- Not HELIOS pipeline evidence

CLI docs: [HelixTest INSTALL](https://github.com/SynapticFour/HelixTest/blob/main/docs/INSTALL.md).
